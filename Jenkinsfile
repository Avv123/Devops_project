pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Avv123/Devops_project'
            }
        }
        stage('Build Backend and Frontend') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Run Services') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
