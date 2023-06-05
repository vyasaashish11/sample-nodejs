pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        // Checkout your source code from version control (e.g., Git)
        git 'https://github.com/vyasaashish11/sample-nodejs.git'
      }
    }
    
    stage('Build') {
      steps {
        // Install dependencies and build the frontend app
        sh 'npm install'
        sh 'npm run build'
      }
    }
    
    stage('Deploy') {
      environment {
        // Set up environment variables required for deployment
        AWS_ACCESS_KEY_ID = 'AKIA5YSPXCQHARQGO7KI'
        AWS_SECRET_ACCESS_KEY = '7ePBRQtwaf4q0cV5ytnzn/R1uPR8wcOa1cZtKmuq'
        AWS_REGION = 'ap-south-1' // Replace with your desired region
        EC2_INSTANCE_ID = 'i-06851d9489ae8dfa6' // Replace with your EC2 instance ID
        S3_BUCKET_NAME = 'bucketfortoday' // Replace with your S3 bucket name
      }
      
      steps {
        // Deploy the frontend app to EC2
        sh '''
          aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
          aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
          aws configure set default.region $AWS_REGION
          aws s3 cp dist/ s3://$S3_BUCKET_NAME/ --recursive
          aws s3 sync --delete s3://$S3_BUCKET_NAME/ /var/www/html/
        '''
      }
    }
  }
}

