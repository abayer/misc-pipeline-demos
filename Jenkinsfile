#!groovy

pipeline {
  agent {
      docker {
          label "docker"
          image "ruby:2.1"
      }
  }  
  options {
    // Keep the 10 most recent builds
    buildDiscarder(logRotator(numToKeepStr:'10')) 
  }
  stages {
    stage ('Build') { 
      steps {
        // install required gems
        sh 'bundle install'

        // build and run tests with coverage
        sh 'bundle exec rake build spec'

        // Archive the built artifacts
        archive includes: 'pkg/*.gem'

        // publish html
        publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'coverage',
            reportFiles: 'index.html',
            reportName: 'RCov Report'
          ]
      }
    }
  }
}
