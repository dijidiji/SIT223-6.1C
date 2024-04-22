pipeline {
    agent any
    environment {
        DIRECTORY_PATH = "some/path"
        TESTING_ENVIRONMENT = "test env"
        PRODUCTION_ENVIRONMENT = "prod env"
    }

    stages {
        stage("Build") {
            steps {
                echo "1. compile code from $DIRECTORY_PATH"
            }
        }
        stage("Test") {
            steps {
                echo "2a. unit tests"
                echo "2b. integration tests"
            }
        }
        stage("Code quality check") {
            steps {
                echo "3. check the quality of the code"
            }
        }
        stage("Deploy") {
            steps {
                echo "4. deploy to $TESTING_ENVIRONMENT"
            }
        }
        stage("Approval") {
            options {
                timeout(time: 15, unit: 'SECONDS')
            }
            steps {
                echo "5a. get approval"
                sleep 10
                echo "5b. approved!"
            }
        }
        stage("Deploy to production") {
            steps {
                echo "6. deploy to $PRODUCTION_ENVIRONMENT"
            }
        }
    }
    post {
        success {
            echo "Pipeline success"
        }
        failure {
            echo "Pipeline fail"
        }
    }
}
