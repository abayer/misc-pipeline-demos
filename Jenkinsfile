pipeline {
    environment {
        // The key here is to not refer to them as ${env.WHATEVER} here but as ${WHATEVER}.
        // Gonna incorporate a fix for that into 1.1.2.
        MICROSERVICE_NAME = "directory"
        IMAGE_NAME = "quay.io/svc/${MICROSERVICE_NAME}"

        IMAGE_ID = "${IMAGE_NAME}:${TAG_NAME}"
        
        // Another note - don't use these "complex" env vars in further env vars! The magic that figures
        // out the right order to resolve environment variables in (which comes from Jenkins core) doesn't
        // seem to know what to do with "${(BRANCH_NAME + "_" + BUILD_ID)}", so TAG_NAME's going to end up 
        // potentially resolving to null, if by luck of the draw it ends up before BRANCH_NAME and BUILD_ID 
        // in withEnv's resolution. Complicated and annoying, I know.
        TAG_NAME = "${(BRANCH_NAME + "_" + BUILD_ID).replaceAll("[.:/\\\\#]", '-')}"
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
