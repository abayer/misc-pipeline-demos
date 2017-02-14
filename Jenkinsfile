pipeline {
    agent {
        docker {
            label "docker"
            image "maven:3.3-jdk-8"
        }
    }

    stages {
        stage("is this real?") {
            steps {
                echo "Oh look, a stage"
            }
        }

        stage("is java installed?") {
            when {
                expression {
                    sh "java -version"
                }
            }
            steps {
                echo "Yup, Java is installed"
            }
        }

        stage("is Maven installed?") {
            when {
                expression {
                    sh "mvn -version"
                }
            }
            steps {
                echo "Yup, Maven is installed"
            }
        }
    }
}