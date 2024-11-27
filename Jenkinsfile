pipeline {
    agent any
    environment {
        DOCKER_BUILDKIT = 1
        API_SECRET_KEY = credentials('api-secret-key') // Fetch the secret key securely
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Avv123/Devops_project.git', branch: 'main'
            }
        }
         stage('Load .env') {
            steps {
                sh '''#!/bin/bash
                export $(cat /home/aryaman-vishnoi/Desktop/openperplex/openperplex_backend_os/.env | xargs)
                # Now the environment variables from .env are available
                echo "MY_VAR is: $MY_VAR"
                '''
            }
        }
        stage('Build Backend and Frontend') {
            steps {
                script {
                    // Make sure to navigate to the folder containing docker-compose.yml
                    dir('path/to/your/docker-compose/folder') {
                        sh 'docker-compose build'
                    }
                }
                
            }
        }
        stage('Run Services') {
            steps {
                script {
                    // Ensure you're in the correct directory where docker-compose.yml is located
                    dir('path/to/your/docker-compose/folder') {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
        stage('Verify Services') {
            steps {
                script {
                    // Check if the services are running properly
                    sh 'docker ps'
                }
            }
        }
    }
    post {
        always {
            cleanWs() // Clean the workspace after the pipeline runs
        }
    }
}
