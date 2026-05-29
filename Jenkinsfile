pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        S3_BUCKET  = 'chirag-static'
        AWS_REGION = 'us-east-1'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Chigich/static-websites-s3.git'
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

