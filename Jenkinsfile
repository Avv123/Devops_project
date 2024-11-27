pipeline {
    agent any
    environment {
        DOCKER_BUILDKIT = 1
        // Using Jenkins credentials (secret API key)
        API_SECRET_KEY = credentials('api-secret-key')
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Avv123/Devops_project.git', branch: 'main'
            }
        }
        
        // Load the .env file and export the variables to the pipeline environment
        stage('Load .env') {
            steps {
                script {
                    // Read .env file and set the environment variables
                    def envFile = '/home/aryaman-vishnoi/Desktop/openperplex/openperplex_backend_os/.env'
                    def envVars = readFile(envFile).split('\n')
                    envVars.each { line ->
                        if (line.trim()) {
                            def (key, value) = line.split('=')
                            if (key && value) {
                                env[key.trim()] = value.trim()
                            }
                        }
                    }
                }
            }
        }

        // Build Backend and Frontend using Docker
        stage('Build Backend and Frontend') {
            steps {
                script {
                    // Ensure Docker Compose uses the correct environment variables
                    dir('path/to/your/docker-compose/folder') {
                        sh 'docker-compose build'
                    }
                }
            }
        }

        // Run the services with Docker Compose
        stage('Run Services') {
            steps {
                script {
                    dir('path/to/your/docker-compose/folder') {
                        // Pass the environment variables to the Docker container
                        sh 'docker-compose up -d'
                    }
                }
            }
        }

        // Verify that the services are running properly
        stage('Verify Services') {
            steps {
                script {
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
