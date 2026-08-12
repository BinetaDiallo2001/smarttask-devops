# SmartTask - Projet DevOps

## Présentation

SmartTask est une application web de gestion de tâches développée dans le cadre d'un projet DevOps.

L'application permet de consulter et d'ajouter des tâches à travers une interface web.

## Architecture

L'application est composée de trois services :

- **Frontend** : interface web de SmartTask
- **Backend** : API REST développée avec Flask
- **Base de données** : MySQL

Les services sont exécutés dans des conteneurs Docker et communiquent à travers un réseau Docker dédié.

## Technologies utilisées

- HTML / CSS / JavaScript
- Python / Flask
- MySQL 8.0
- Docker
- Docker Compose
- Git
- GitHub

## Structure du projet

```text
smarttask-devops/
├── backend/
│   ├── app.py
│   ├── Dockerfile
│   └── requirements.txt
│
├── frontend/
│   ├── index.html
│   └── Dockerfile
│
├── docker-compose.yml
└── README.md
