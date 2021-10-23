pipeline {
  agent any
  stages {
    stage('Setup Environment') {
      steps {
        sh 'curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3'
        sh "$HOME/.poetry/bin/poetry install --no-root"
      }
    }

    stage('Code Style') {
      steps {
        sh './pants lint ::'
      }
    }

    stage('UnitTesting') {
      steps {
        sh './pants test --use-coverage --coverage-py-report="xml" ::'
      }
    }

    stage('Packaging') {
      steps {
        sh './pants package ::'
      }
    }

    stage('Deploy Infrastructure') {
      steps {
        echo 'Update/Network Overlay-Network'
        sh 'docker network inspect beehive_dev_network >/dev/null 2>&1 || docker network create -d overlay  beehive_dev_network'
      }
    }

  }
  post {
    always {
      junit(allowEmptyResults: true, testResults: 'dist/pytest_results/**/*.xml')
      publishCoverage(adapters: [coberturaAdapter('dist/coverage/python/coverage.xml'), jacocoAdapter('**/target/site/jacoco/jacoco.xml')], sourceFileResolver: sourceFiles('NEVER_STORE'))
    }

  }
}