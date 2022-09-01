pipeline {
  agent any
  environment {
    dockerhub=credentials('dockerhub')
  }
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/naleruto1234/naleruto1234.git', branch: 'master')
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t naleruto/nale-jenkins:latest .'
      }
    }

    stage('Release') {
      steps {
        echo 'Ready to release etc.'
      }
    }

  }
}