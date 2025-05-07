pipeline {
  agent any
  environment {
    IMAGE_TAG = "${BUILD_NUMBER}"
    AWS_REGION = "us-west-2"
    EKS_CLUSTER = "automode-cluster"
  }
  stages {
    stage('Build') {
      steps {
        sh 'echo Build I am in `pwd`, with BUILD_NUMBER ${BUILD_NUMBER}'
      }
    }
    stage('Push') {
      steps {
        sh 'echo PUSH I am in `pwd`, with BUILD_NUMBER ${BUILD_NUMBER}'
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
}
