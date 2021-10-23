pipeline {
  agent any
  stages {
    stage('Code Style') {
      steps {
        echo 'Checking Code Style'
        sh '''poetry install
poetry shell
./pants lint ::'''
      }
    }

  }
}