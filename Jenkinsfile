pipeline {

  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
  }

  agent {
    label ''
  }

  environment {
    REST_API_URL = "${env.BRANCH_NAME == 'master' ? 'https://one-url' : 'https://two-url'}"
  }

  stages {
    stage('foo') {
      when {
        expression {
          echo "Branch: ${env.BRANCH_NAME}"
          return env.BRANCH_NAME == "pants" || env.BRANCH_NAME == "jenkins-42498"
        }
      }
      steps {
        echo "Hi there, ${env.REST_API_URL}"
      }
    }
  }
}
