pipeline {
  agent {
        docker { image 'node:14-alpine' }
    }
  stages {
    stage('Setup Environment') {
            steps {
                sh 'apt-get update && apt-get install -y curl'
                sh "curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python"
                sh "$HOME/.poetry/bin/poetry install --no-root"
            }
    }
    stage('Code Style') {
      steps {
        sh "./pants lint ::"
      }
    }

  }
}