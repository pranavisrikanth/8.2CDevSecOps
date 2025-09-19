pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN') // Your SonarCloud token securely loaded from Jenkins
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test || echo "Tests failed but continuing..."'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running npm audit...'
                sh 'npm audit || echo "Audit found issues"'
            }
        }

        // 🔽 This is where you add the SonarCloud Analysis stage
        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        echo "Downloading SonarScanner CLI..."
                        curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006.zip
                        unzip -q sonar-scanner.zip
                        export PATH=$PATH:$PWD/sonar-scanner-5.0.1.3006/bin

                        echo "Running SonarCloud Analysis..."
                        sonar-scanner -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}
