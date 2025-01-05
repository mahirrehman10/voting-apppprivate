pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/mahirrehman10/voting-appprivate.git' // Repository URL
        DOCKER_IMAGE_NAME = 'taskupgarde'                                 // Docker Image Name
        ECR_REPOSITORY = '879576034845.dkr.ecr.us-east-1.amazonaws.com/taskupgarde/voteapp' // ECR Repository URL
        AWS_REGION = 'us-east-1'                                          // AWS Region
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking out repository..."
                    git branch: 'main', url: "${env.REPO_URL}", credentialsId: 'github-credentials-id'
                }
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-credentials-id', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    script {
                        echo "Building Docker Image..."
                        sh "docker build -t ${env.DOCKER_IMAGE_NAME}:latest ."

                        echo "Logging in to ECR..."
                        sh "aws ecr get-login-password --region ${env.AWS_REGION} | docker login --username AWS --password-stdin ${env.ECR_REPOSITORY}"

                        echo "Tagging and Pushing Docker Image..."
                        sh "docker tag ${env.DOCKER_IMAGE_NAME}:latest ${env.ECR_REPOSITORY}:latest"
                        sh "docker push ${env.ECR_REPOSITORY}:latest"
                    }
                }
            }
        }
    }
}
