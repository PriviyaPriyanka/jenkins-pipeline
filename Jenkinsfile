pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Docker image') {
      steps {
        sh 'docker build -t git-project:latest .'
      }
    }
    stage('Run container') {
      steps {
        sh 'docker run git-project:latest'
      }
    }
  }
}
