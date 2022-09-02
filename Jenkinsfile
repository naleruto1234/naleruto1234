pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/naleruto1234/naleruto1234.git', branch: 'master')
      }
    }

    stage('Build Docker Image') {
      steps {
        echo 'Build Docker Image.'
      }
    }

    stage('Run Docker Image') {
      steps {
        echo 'Run Docker Image.'
      }
    }

    stage('Test Project') {
      steps {
        echo 'Test Project.'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy.'
      }
    }

    stage('Release') {
      steps {
        echo 'Ready to release etc.'
      }
    }

  }
}