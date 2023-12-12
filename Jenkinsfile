pipeline {
    agent any

   

    stages {
        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build --no-cache -t gatewayms/api -f Dockerfile .'
                }
            }
        }

        stage('Push and Deploy') {
            steps {
                script {
                    // Stop and remove existing container (if any)
                    sh 'docker stop gatewayms || true && docker rm gatewayms || true'

                    // Run a new container with the built image
                    sh 'docker run -d --name gatewayms -p 5000:80 --env "ASPNETCORE_ENVIRONMENT=Development" gatewayms/api:latest'
                }
            }
        }
    }
}
