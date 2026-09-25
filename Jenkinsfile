pipeline {
    agent any

    environment {
        S3_BUCKET = 'phani-bucket-jack'
        AWS_REGION = 'us-east-1'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kvsphani548-coder/demo.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                    aws s3 sync . s3://$S3_BUCKET \
                        --exclude ".git/*" \
                        --exclude "Jenkinsfile" \
                        --delete \
                        --region $AWS_REGION
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment to S3 successful!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}
