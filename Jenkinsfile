pipeline {
  agent any
  stages {
    stage('Code Style') {
      steps {
        echo 'Checking Code Style'
        sh './pants lint ::'
      }
    }

  }
}