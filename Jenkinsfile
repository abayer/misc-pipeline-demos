pipeline {
    environment {
        MICROSERVICE_NAME = "directory"
        IMAGE_NAME = "quay.io/svc/${env.MICROSERVICE_NAME}"

        IMAGE_ID = "${env.IMAGE_NAME}:${env.TAG_NAME}"
        TAG_NAME = "${(env.BRANCH_NAME + "_" + env.BUILD_ID).replaceAll("[.:/\\\\#]", '-')}"
    }
    agent {
        label "some-label"
    }

    stages {
        stage("foo") {
            steps {
                sh 'echo "MICROSERVICE_NAME is ${env.MICROSERVICE_NAME}"'
                sh 'echo "IMAGE_NAME is ${env.IMAGE_NAME}"'
                sh 'echo "IMAGE_ID is ${env.IMAGE_ID}"'
                sh 'echo "TAG_NAME is ${env.TAG_NAME}"'
            }
        }
    }
}
