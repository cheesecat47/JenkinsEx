pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker {
                    image 'maven:3.9.6-eclipse-temurin-17-alpine'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                sh 'echo "build"'
                sh 'uname -a'
                sh 'mvn --version'
            }
        }
    }
    post {
        success {
            script {
                def AUTHOR_ID = sh(script: "git show -s --pretty=%an", returnStdout: true).trim()
                def AUTHOR_NAME = sh(script: "git show -s --pretty=%ae", returnStdout: true).trim()
                mattermostSend (
                    color: 'good',
                    message: "Succeed to build: ${env.JOB_NAME} #${env.BUILD_NUMBER} by ${AUTHOR_ID}(${AUTHOR_NAME})\n(<${env.BUILD_URL}|Details>)",
                    endpoint: 'https://meeting.ssafy.com/hooks/63piomqgsjyf9mshb7wxsy4yuo',
                    channel: 'D112-Alert'
                )
            }
        }
        failure {
            script {
                def AUTHOR_ID = sh(script: "git show -s --pretty=%an", returnStdout: true).trim()
                def AUTHOR_NAME = sh(script: "git show -s --pretty=%ae", returnStdout: true).trim()
                mattermostSend (
                    color: 'danger',
                    message: "Failed to build: ${env.JOB_NAME} #${env.BUILD_NUMBER} by ${AUTHOR_ID}(${AUTHOR_NAME})\n(<${env.BUILD_URL}|Details>)",
                    endpoint: 'https://meeting.ssafy.com/hooks/63piomqgsjyf9mshb7wxsy4yuo',
                    channel: 'D112-Alert'
                )
            }
        }
    }
}
