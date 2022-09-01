pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/naleruto1234/naleruto1234.git', branch: 'master')
      }
    }

    stage('Docker Build') {
      agent { dockerfile true }
      steps {
        echo 'Build.'
      }
    }

    stage('Release') {
      steps {
        echo 'Ready to release etc.'
      }
    }

  }
}