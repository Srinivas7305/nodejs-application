pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                sh 'node --version'
                sh 'npm --version'
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }
    node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonar-npm';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-npm"
    }
  }
}

    post {
        success {
            archiveArtifacts artifacts: 'dist/**', fingerprint: true
        }
    }
}
