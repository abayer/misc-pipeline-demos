def getCount() { return 10 }
pipeline {

  options {
    buildDiscarder(logRotator(numToKeepStr: "${defCount()}"))
  }

  agent {
    label ''
  }

  environment {
    REST_API_URL = "pants"
  }

  stages {
    stage('foo') {
      when {
        branch "jenkins-42498"
      }
      steps {
        echo "Hi there, ${env.REST_API_URL}"
      }
    }
    stage('bar') {
      when {
        expression {
          echo "REST_API_URL: ${REST_API_URL}"
          return true
        }
      }
      steps {
        echo "Huh"
      }
    }
  }
}
