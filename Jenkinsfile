pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/mahirrehman10/voting-appprivate.git'
        BRANCH_NAME = 'main'
        DOCKER_IMAGE_NAME = 'taskupgarde'
        ECR_REGISTRY = '879576034845.dkr.ecr.us-east-1.amazonaws.com'
        ECR_REPOSITORY = 'taskupgarde/voteapp'
    }
    parameters {
        string(name: 'COMMIT_ID', defaultValue: 'HEAD', description: 'Commit ID to checkout')
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub using HTTPS and credentials
                git branch: "${params.BRANCH_NAME}", url: "${env.REPO_URL}", credentialsId: 'your-credentials-id'
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build("${env.DOCKER_IMAGE_NAME}:latest", '.')

                    // Login to ECR
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${env.ECR_REGISTRY}"

                    // Tag and Push the Docker image
                    sh "docker tag ${env.DOCKER_IMAGE_NAME}:latest ${env.ECR_REGISTRY}/${env.ECR_REPOSITORY}:latest"
                    sh "docker push ${env.ECR_REGISTRY}/${env.ECR_REPOSITORY}:latest"
                }
            }
        }
    }
}
