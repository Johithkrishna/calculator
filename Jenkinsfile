pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="409443329347"
        AWS_DEFAULT_REGION="us-east-1"
        IMAGE_REPO_NAME="practise_123"
        IMAGE_TAG="v1"
        REPOSITORY_URI = "409443329347.dkr.ecr.us-east-1.amazonaws.com/practise_123"
    }
   
    stages {
        
         stage('Logging into AWS ECR') {
            steps {
                script {
                sh """aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"""
                }
                 
            }
        }
        
        stage('Checkout') {
            steps {
                // Checkout the source code from your version control system
                git 'https://github.com/Johithkrishna/calculator.git'
            }
        }
  
       // Building Docker images
       stage('Building image') {
       steps{
        script {
          dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
             }
           }
       }
   
        // Uploading Docker images into AWS ECR
        stage('Pushing to ECR') {
          steps{  
         script {
                sh """docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${REPOSITORY_URI}:$IMAGE_TAG"""
                sh """docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"""
         }
        }
      }
    }
}