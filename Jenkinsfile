pipeline {
    agent {
        docker {
            image 'node:16-alpine'
        }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install --save'
            }
        }
        stage('Install Snyk Locally') {
            steps {
                sh 'npm install snyk'
            }
        }
        stage('Security Scan') {
            steps {
                sh './node_modules/.bin/snyk test'
            }
        }
    }
}
