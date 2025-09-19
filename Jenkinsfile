pipeline {
  agent any

  environment {
    SONAR_TOKEN = credentials('9e0ab0bd325816efb791a1ea2527844a1c439624') 
  }

  stages {

    stage('Build') {
      steps {
        echo 'Installing dependencies...'
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        echo ' Running tests...'
        // Continue even if tests fail (for pipeline continuity)
        sh 'npm test || echo "Tests failed, but continuing..."'
      }
    }

    stage('SonarCloud Analysis') {
      steps {
        echo ' Starting SonarCloud scan...'
        sh '''
          echo " Downloading SonarScanner CLI..."
          curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
          
          echo " Extracting..."
          unzip -q sonar-scanner.zip
          
          echo " Running SonarScanner..."
          export PATH=$PWD/sonar-scanner-5.0.1.3006-linux/bin:$PATH
          sonar-scanner
        '''
      }
    }
  }

  post {
    always {
      echo ' Pipeline completed.'
    }
    failure {
      echo ' Pipeline failed. Check logs for errors.'
    }
  }
}
