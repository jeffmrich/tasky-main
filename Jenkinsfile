pipeline {
  agent any
  environment {
    IMAGE_TAG = "${BUILD_NUMBER}"
    AWS_REGION = "us-west-2"
    EKS_CLUSTER = "automode-cluster"
  }
  stages {
    stage('Build image') {
      steps {
        sh 'docker build -t tasky:${IMAGE_TAG} .'
      }
    }
    stage('Auth, tag, and push to ECR') {
      steps {
        sh 'echo Auth'
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
        credentialsId: 'b2a7bcce-5b43-48e9-a8e3-ea75faa01903',
        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) { 
            sh 'aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 650251718485.dkr.ecr.us-west-2.amazonaws.com'
        }
        sh 'echo Tag'
        sh 'docker tag tasky:${IMAGE_TAG} 650251718485.dkr.ecr.us-west-2.amazonaws.com/tasky:${IMAGE_TAG}'
        sh 'echo Push to ECR'
        sh 'docker push 650251718485.dkr.ecr.us-west-2.amazonaws.com/tasky:${IMAGE_TAG}'
      }
    }
    stage('Update Manifest') {
      steps {
        sh 'echo Update Manifest I am in `pwd`, with IMAGE_TAG ${IMAGE_TAG}'
        sh 'sed -i "s|amazonaws.com/tasky:.*|amazonaws.com/tasky:${IMAGE_TAG}|" tasky.yaml'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo Deploy I am in `pwd`, with IMAGE_TAG ${IMAGE_TAG}'
        }
      }
    }
}
