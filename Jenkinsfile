pipeline {
    agent any
    stages {
         stage('Checkout') {
            steps {
                git url: 'https://github.com/Avv123/Devops_project.git', branch: 'main'
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
