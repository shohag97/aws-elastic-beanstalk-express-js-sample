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
        stage('Security Scan') {
            steps {
                sh 'npm install -g snyk'
                sh 'snyk test --severity-threshold=high'
            }
        }
    }
}
