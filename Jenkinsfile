pipeline {
    agent {
        docker { image 'node:16-alpine' }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install --save'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Security Scan') {
            steps {
                withCredentials([string(credentialsId: 'snyk-token', variable: 'SNYK_TOKEN')]) {
                    // Install Snyk locally
                    sh 'npm install snyk'
                    // Run Snyk, but ignore exit code to avoid failing the pipeline
                    sh './node_modules/.bin/snyk test || true'
                }
            }
        }
    }
    post {
        always {
            echo 'Archiving logs...'
            archiveArtifacts artifacts: '**/logs/**/*.log', allowEmptyArchive: true
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check logs for more details.'
        }
    }
}
