pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/mahirrehman10/voting-appprivate.git'
        DOCKER_IMAGE_NAME = 'taskupgarde'
        ECR_REPOSITORY = '879576034845.dkr.ecr.us-east-1.amazonaws.com/taskupgarde/voteapp'
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                git branch: 'main', url: "${env.REPO_URL}", credentialsId: 'your-credentials-id'
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build("${env.DOCKER_IMAGE_NAME}:latest", '.')

                    // Login to ECR and push the Docker image
                    sh """
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${env.ECR_REPOSITORY}
                    docker tag ${env.DOCKER_IMAGE_NAME}:latest ${env.ECR_REPOSITORY}:latest
                    docker push ${env.ECR_REPOSITORY}:latest
                    """
                }
            }
        }
    }
}
