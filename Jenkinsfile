pipeline {
  agent any
  environment {
    IMAGE_NAME = "priviya/git-project"
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Docker image') {
      steps {
        sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
      }
    }
    stage('Docker login') {
      steps {
        withCredentials( [usernamePassword(
          credentialsId: 'dockerhub-creds',
          usernameVariable: 'DOCKER_USER',
          passwordVariable: 'DOCKER_PASS'
          )]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
        }
      }
    }
    stage('Push Image') {
      steps {
        sh 'docker push $IMAGE_NAME:$BUILD_NUMBER'
      }
    }
    stage('Cleanup') {
      steps {
        sh 'docker image prune -f'
      }
    }
  }
}
