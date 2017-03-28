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
                echo "MICROSERVICE_NAME is ${env.MICROSERVICE_NAME}"
                echo "IMAGE_NAME is ${env.IMAGE_NAME}"
                echo "IMAGE_ID is ${env.IMAGE_ID}"
                echo "TAG_NAME is ${env.TAG_NAME}"
            }
        }
    }
}
