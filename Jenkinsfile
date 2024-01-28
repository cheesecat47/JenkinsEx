pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                sh 'echo "docker compose up -d"'
                sh 'docker-compose up -d backend'
            }
        }
    }

    post {
        success {
            script {
                def AUTHOR_ID = sh(script: 'git show -s --pretty=%an', returnStdout: true).trim()
                def AUTHOR_NAME = sh(script: 'git show -s --pretty=%ae', returnStdout: true).trim()
                mattermostSend(
                    color: 'good',
                    message: "Succeed to build: ${env.JOB_NAME} #${env.BUILD_NUMBER} by ${AUTHOR_ID}(${AUTHOR_NAME})\n(${env.BUILD_URL}|Details)",
                    endpoint: 'https://meeting.ssafy.com/hooks/63piomqgsjyf9mshb7wxsy4yuo',
                    channel: 'D112-Alert',
                    icon: 'http://i10d112.p.ssafy.io:18080/static/a7112f41/images/svgs/logo.svg'
                )
            }
        }
        failure {
            script {
                def AUTHOR_ID = sh(script: 'git show -s --pretty=%an', returnStdout: true).trim()
                def AUTHOR_NAME = sh(script: 'git show -s --pretty=%ae', returnStdout: true).trim()
                mattermostSend(
                    color: 'danger',
                    message: "Failed to build: ${env.JOB_NAME} #${env.BUILD_NUMBER} by ${AUTHOR_ID}(${AUTHOR_NAME})\n(${env.BUILD_URL}|Details)",
                    endpoint: 'https://meeting.ssafy.com/hooks/63piomqgsjyf9mshb7wxsy4yuo',
                    channel: 'D112-Alert',
                    icon: 'http://i10d112.p.ssafy.io:18080/static/a7112f41/images/svgs/logo.svg'
                )
            }
        }
    }
}
