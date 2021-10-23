pipeline {
  agent any
  stages {
    stage('Setup Environment') {
            steps {
                sh "curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3"
                sh "$HOME/.poetry/bin/poetry install --no-root"
            }
    }
    stage('Code Style') {
      steps {
        sh "./pants lint ::"
      }
    }

    stage('UnitTesting') {
      steps {
        sh './pants test --use-coverage --coverage-py-report="xml" ::'
      }
    }

    stage('Packaging') {
      steps {
        sh "./pants package ::"
      }
    }

  }
  post {
        always {
            junit 'dist/coverage/**/*.xml'
        }
    }
}
