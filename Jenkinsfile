pipeline {
    agent any
    
    environment {
        DOCKER_BUILDKIT = 1
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Avv123/Devops_project.git', branch: 'main'
            }
        }
        
        stage('Prepare Secrets') {
            steps {
                script {
                    withCredentials([
                        string(credentialsId: 'cohere-api-key', variable: 'COHERE_API_KEY'),
                        string(credentialsId: 'groq-api-key', variable: 'GROQ_API_KEY'),
                        string(credentialsId: 'jina-api-key', variable: 'JINA_API_KEY'),
                        string(credentialsId: 'serper-api-key', variable: 'SERPER_API_KEY')
                    ]) {
                        writeFile file: 'openperplex_backend_os/.env', text: """
COHERE_API_KEY=${COHERE_API_KEY}
GROQ_API_KEY=${GROQ_API_KEY}
JINA_API_KEY=${JINA_API_KEY}
SERPER_API_KEY=${SERPER_API_KEY}
"""
                    }
                }
            }
        }

        stage('Debug .env Content') {
            steps {
                script {
                    sh 'cat openperplex_backend_os/.env'
                }
            }
        }
        
        stage('Build Backend and Frontend') {
            steps {
                script {
                    sh 'docker-compose build'
                }
            }
        }
        
        stage('Run Services') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }
        
        stage('Check Backend Logs') {
            steps {
                script {
                    sh 'docker-compose logs backend'
                }
            }
        }

        stage('Verify Services') {
            steps {
                script {
                    sh 'docker ps'
                    sh '''
                        docker-compose ps
                        docker-compose logs backend
                        docker-compose logs frontend
                    '''
                }
            }
        }
    }
}
