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
            post {
                always {
                    emailext body: "Emailext test",
                        subject: "Emailext test",
                        to: "danleecarroll@gmail.com"
                }
            }
        }
        stage("Code quality check") {
            steps {
                echo "3. check the quality of the code"
            }
        }
        stage("Security scan") {
            steps {
                echo "4. Perform security scan on code"
            }
            post {
                always {
                    echo "TODO: email notification"
                }
            }
        }
        stage("Deploy to staging") {
            steps {
                echo "5. deploy to $TESTING_ENVIRONMENT"
            }
        }
        stage("Staging tests") {
            steps{
                echo "6. run integration tests on $TESTING_ENVIRONMENT"
            }
        }
        stage("Deploy to production") {
            steps {
                echo "7. deploy to $PRODUCTION_ENVIRONMENT"
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
