pipeline {
    agent {
        label 'docker-agent'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t BinetaDiallo2001/smarttask-backend:latest ./backend'
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'docker build -t BinetaDiallo2001/smarttask-frontend:latest ./frontend'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USER" --password-stdin'
                }
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push BinetaDiallo2001/smarttask-backend:latest'
                sh 'docker push BinetaDiallo2001/smarttask-frontend:latest'
            }
        }
    }

    post {
        always {
            echo 'Fin de l’exécution du pipeline.'
        }
        success {
            echo 'Pipeline CI/CD terminé avec succès.'
        }
        failure {
            echo 'Le pipeline a échoué.'
        }
    }
}
