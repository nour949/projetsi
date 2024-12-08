pipeline {
    agent any

    environment {
        FRONTEND_DIR = 'front'
        BACKEND_DIR = 'back'
        FRONTEND_IMAGE = 'frontend-image'
        BACKEND_IMAGE = 'backend-image'
        FRONTEND_PORT = '8083'
        BACKEND_PORT = '8082'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/nour949/projetsi', branch: 'main'
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir("ui") {
                    script {
                        bat "docker build -t ui ."
                    }
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir("back") {
                    script {
                        bat "docker build -t back ."
                    }
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                script {
                    // Stop and remove existing frontend container =
                    bat "docker stop ui || true"
                    bat "docker rm ui|| true"
                    
                    // Run the frontend container
                    bat "docker run -d  --network bis_network --name ui -p 8081:80 ui"
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                script {
                    // Stop and remove existing backend container if exists
                    bat "docker stop back || true"
                    bat "docker rm back || true"
                    
                    // Run the backend container
                    bat "docker run -d  --network bis_network --name back -p 8082:443 back"
                }
            }
        }
    }

    post {
        always {
            echo 'Deployment finished.'
        }
    }
}