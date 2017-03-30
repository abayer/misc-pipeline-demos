@Library('fxtest@submitToTreeherder') _


/** Desired capabilities */
def capabilities = [
  browserName: 'Firefox',
  version: '47.0',
  platform: 'Windows 10'
]

pipeline {
  agent any
  options {
    timestamps()
    timeout(time: 1, unit: 'HOURS')
  }
  environment {
    /** See https://issues.jenkins-ci.org/browse/JENKINS-42771 - we'd like to expand this out into multi-line concatenations */
    PYTEST_ADDOPTS = "-n=10 --tb=short --color=yes --driver=SauceLabs --variables=capabilities.json --log-raw=results/py27_raw.txt --log-tbpl=results/py27_tbpl.txt"
    PULSE = "HEY HERE"
    SAUCELABS_API_KEY = "HEY THERE"
  }
  stages {
    stage('Lint') {
      steps {
        sh "echo tox -e flake8"
      }
    }
    stage('Test') {
      steps {
        writeCapabilities(capabilities, 'capabilities.json')
        sh "echo tox -e py27"
        echo 'pre-submitToTreeherder'
        submitToTreeherder(
          project: 'fxapom',
          jobSymbol: 'T',
          jobName: 'Tests')
        echo 'post-submitToTreeherder'
      }
    }
  }
}
