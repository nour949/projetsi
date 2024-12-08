pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/nour949/projetsi', branch: 'main'
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir("ui") {  // Ensure 'ui' directory contains the frontend Dockerfile
                    script {
                        bat "docker build -t ui ."
                    }
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir("nginx") {  // Ensure 'nginx' directory contains the backend Dockerfile
                    script {
                        bat "docker build -t back ."
                    }
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                script {
                    // Stop and remove existing frontend container if exists
                    bat "docker stop ui || true"
                    bat "docker rm ui || true"
                    
                    // Run the frontend container
                    bat "docker run -d --network bis_network --name ui -p 8081:80 ui"
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
                    bat "docker run -d --network bis_network --name back -p 8082:443 back"
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
