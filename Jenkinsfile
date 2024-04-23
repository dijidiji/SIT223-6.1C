pipeline {
    agent any
    environment {
        DIRECTORY_PATH = "git/repo"
        TESTING_ENVIRONMENT = "EC2 test"
        PRODUCTION_ENVIRONMENT = "EC2 prod"
    }

    stages {
        stage("Build") {
            steps {
                echo "1. Gradle build from $DIRECTORY_PATH"
            }
        }
        stage("Test") {
            steps {
                echo "2. Junit unit and integration testing"
            }
            post {
                always {
                    emailext (
                        from: 'Local Jenkins <danleecarroll@gmail.com>',
                        to: 'danleecarroll@gmail.com',
                        subject: '$PROJECT_NAME - Test - Build # $BUILD_NUMBER - $BUILD_STATUS!',
                        body: '$GIT_BRANCH $GIT_REVISION - Build # $BUILD_NUMBER - $BUILD_STATUS! Build log is attached.',
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        stage("Code quality check") {
            steps {
                echo "3. SonarQube code quality check"
            }
        }
        stage("Security scan") {
            steps {
                echo "4. SonarQube security scan"
            }
            post {
                always {
                    emailext (
                        from: 'Local Jenkins <danleecarroll@gmail.com>',
                        to: 'danleecarroll@gmail.com',
                        subject: '$PROJECT_NAME - Security scan - Build # $BUILD_NUMBER - $BUILD_STATUS!',
                        body: '$GIT_BRANCH $GIT_REVISION - Build # $BUILD_NUMBER - $BUILD_STATUS! Build log is attached.',
                        attachLog: true,
                        compressLog: true
                    )
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
                echo "6. run production integration tests on $TESTING_ENVIRONMENT"
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
