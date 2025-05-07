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
        sh 'docker build -t myrepo/my-app:${IMAGE_TAG} .'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push myrepo/my-app:${IMAGE_TAG}'
      }
    }
    stage('Update Manifest') {
      steps {
        sh 'sed -i "s|image: myrepo/my-app:.*|image: myrepo/my-app:${IMAGE_TAG}|" k8s/deployment.yaml'
      }
    }
    stage('Deploy') {
      steps {
        withAWS(credentials: 'AWS-CREDS', region: "${AWS_REGION}") {
          sh 'aws eks update-kubeconfig --name ${EKS_CLUSTER} --region ${AWS_REGION}'
          sh 'kubectl apply -f k8s/deployment.yaml'
        }
      }
    }
  }
}
