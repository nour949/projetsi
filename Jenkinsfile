pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/nour949/projetsi', branch: 'main'
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
