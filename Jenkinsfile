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
                        body: "The Test stage completed with status: ${currentBuild.currentResult}"
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                bat 'npm audit || exit 0'
            }
            post {
                always {
                    emailext (
                        to: 'pranavisrikanth6@gmail.com',
                        subject: "Security Scan: ${currentBuild.currentResult}",
                        body: "Security scan completed with status: ${currentBuild.currentResult}"
                    )
                }
            }
        }
    }
}
