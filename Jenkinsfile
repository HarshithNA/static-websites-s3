pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        S3_BUCKET  = 's3-bucket-october-batch'
        AWS_REGION = 'eu-north-1'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/HarshithNA/static-websites-s3'
            }
        }
        stage('Deploy') {
            steps {
                sh 'aws s3 cp index.html s3://$S3_BUCKET/index.html --region $AWS_REGION'
            }
        }
    }
    post {
        success { echo "Deployed to s3://$S3_BUCKET/" }
        failure { echo "Failed — check ${env.BUILD_URL}" }
    }
}

