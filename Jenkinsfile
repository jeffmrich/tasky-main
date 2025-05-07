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
    stage('Tag and push to ECR') {
      steps {
        sh 'echo Tag'
        sh 'docker tag tasky:${BUILD_NUMBER} 650251718485.dkr.ecr.us-west-2.amazonaws.com/tasky:${BUILD_NUMBER}'
        sh 'echo Push to ECR'
        sh 'docker push 650251718485.dkr.ecr.us-west-2.amazonaws.com/tasky:${BUILD_NUMBER}'
      }
    }
    stage('Update Manifest') {
      steps {
        sh 'echo Update Manifest I am in `pwd`, with BUILD_NUMBER ${BUILD_NUMBER}'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo Deploy I am in `pwd`, with BUILD_NUMBER ${BUILD_NUMBER}'
        }
      }
    }
}
