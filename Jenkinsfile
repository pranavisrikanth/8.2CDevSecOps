pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
            post {
                always {
                    emailext (
                        to: 'pranavisrikanth6@gmail.com',
                        subject: "Test Stage: ${currentBuild.currentResult}",
                        body: "Test stage completed with status: ${currentBuild.currentResult}",
                        attachmentsPattern: '**/test-results/*.log',
                        mimeType: 'text/plain'
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
            }
            post {
                always {
                    emailext (
                        to: 'pranavisrikanth6@gmail.com',
                        subject: "Security Scan Stage: ${currentBuild.currentResult}",
                        body: "Security scan completed with status: ${currentBuild.currentResult}",
                        attachmentsPattern: '**/security/*.log',
                        mimeType: 'text/plain'
                    )
                }
            }
        }
    }
}
