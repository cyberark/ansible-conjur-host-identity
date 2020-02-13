#!/usr/bin/env groovy

pipeline {
  agent { label 'executor-v2' }

  options {
    timestamps()
    buildDiscarder(logRotator(daysToKeepStr: '14'))
  }

  triggers {
    cron(getDailyCronString())
  }

  stages {
    stage('Validate Changelog') {
      steps { sh './tests/parse-changelog.sh' }
    }

    stage('Run tests') {
      steps {
        sh 'cd tests; ./test.sh'

        junit 'tests/junit/*'
      }
    }

  }

  post {
    always {
      cleanupAndNotify(currentBuild.currentResult)
    }
  }
}
