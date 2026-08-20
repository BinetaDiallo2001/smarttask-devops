pipeline {
    agent {
        label 'docker-agent'
    }

    environment {
        DOCKER_USER = 'bineta2026'
        BACKEND_IMAGE = 'bineta2026/smarttask-backend:latest'
        FRONTEND_IMAGE = 'bineta2026/smarttask-frontend:latest'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t $BACKEND_IMAGE ./backend'
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'docker build -t $FRONTEND_IMAGE ./frontend'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'docker-password',
                        variable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                        -u "$DOCKER_USER" \
                        --password-stdin
                    '''
                }
            }
        }

        stage('Push Images') {
            steps {
                sh '''
                    docker push $BACKEND_IMAGE
                    docker push $FRONTEND_IMAGE
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline CI/CD exécuté avec succès !'
            echo 'Les images Docker ont été construites et poussées vers Docker Hub.'
        }

        failure {
            echo 'Le pipeline a échoué.'
        }

        always {
            echo 'Fin de l’exécution du pipeline.'
        }
    }
}

