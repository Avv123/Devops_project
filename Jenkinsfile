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
                    // Dynamically create .env file with multiple API keys
                    withCredentials([
                        string(credentialsId: 'cohere-api-key', variable: 'COHERE_API_KEY'),
                        string(credentialsId: 'groq-api-key', variable: 'GROQ_API_KEY'),
                        string(credentialsId: 'jina-api-key', variable: 'JINA_API_KEY'),
                        string(credentialsId: 'serper-api-key',variable:'SERPER_API_KEY')
                    ]) {
                        // Create .env file in backend directory
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
        
        stage('Build Backend and Frontend') {
            steps {
                script {
                    // Build using docker-compose
                    sh 'docker-compose build'
                }
            }
        }
        
        stage('Run Services') {
            steps {
                script {
                    // Start services in detached mode
                    sh 'docker-compose up -d'
                }
            }
        }
        
        stage('Verify Services') {
            steps {
                script {
                    // Check running containers
                    sh 'docker ps'
                    
                    // Optional: Add health checks
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