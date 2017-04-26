pipeline {
    agent none
    
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Git branch to use for the build.')
        choice(name: 'APPEND_COMMIT_VERSION', choices: 'ON\nOFF', description: 'Append Git commit ID to build version?')
        choice(name: 'DEBUG_SQL', choices: '0\n1\n2', description: 'Level of SQL tracing.\n0 - disabled.')
        choice(name: 'SAP_CONNECTION_POOL_DEBUG', choices: '0\n1', description: 'Level of SAP connection pool tracing.\nWorks only in debug builds.\n0 - disabled.')
        choice(name: 'BUILD_TYPE', choices: 'RelWithDebInfo\nDebug\nRelease', description: 'Build type')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '1000'))
    }


    stages {
        stage('huh') {
            steps {
                sleep 5
                echo "branch? ${params.BRANCH}"
            }
        }
    }
}
