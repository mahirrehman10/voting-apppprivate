pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Check out the code from your repository
                git branch: 'main', 
                    credentialsId: 'your-credentials-id', 
                    url: 'https://github.com/mahirrehman10/voting-appprivate.git'
            }
        }

        stage('Check Environment') {
            steps {
                // Print environment details to verify the setup
                echo 'Jenkins pipeline setup is successful!'
                sh 'echo "Running on node: $(hostname)"'
                sh 'java -version || echo "Java is not installed"'
            }
        }

        stage('Finish') {
            steps {
                // Final message to confirm the pipeline completed
                echo 'Pipeline completed successfully!'
            }
        }
    }
}
