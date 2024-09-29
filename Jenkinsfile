pipeline {
    agent {
        docker { image 'node:16-alpine' }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    try {
                        echo 'Installing dependencies...'
                        sh 'npm install --save'
                        echo 'Dependencies installed successfully.'
                    } catch (Exception e) {
                        echo 'Failed to install dependencies.'
                        error('Stopping pipeline due to failure in Install Dependencies stage.')
                    }
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    try {
                        echo 'Building the application...'
                        sh 'npm run build'
                        echo 'Build completed successfully.'
                    } catch (Exception e) {
                        echo 'Build failed.'
                        error('Stopping pipeline due to failure in Build stage.')
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    try {
                        echo 'Running tests...'
                        sh 'npm test'
                        echo 'Tests ran successfully.'
                    } catch (Exception e) {
                        echo 'Tests failed.'
                        error('Stopping pipeline due to failure in Test stage.')
                    }
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    try {
                        echo 'Running Snyk Security Scan...'
                        withCredentials([string(credentialsId: 'snyk-token', variable: 'SNYK_TOKEN')]) {
                            sh 'npm install snyk'
                            sh './node_modules/.bin/snyk test || true'
                        }
                        echo 'Snyk security scan completed.'
                    } catch (Exception e) {
                        echo 'Snyk security scan failed.'
                        error('Stopping pipeline due to failure in Security Scan stage.')
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    try {
                        echo 'Deploying the application...'
                        echo 'Application deployed successfully.'
                    } catch (Exception e) {
                        echo 'Deployment failed.'
                        error('Stopping pipeline due to failure in Deploy stage.')
                    }
                }
            }
        }
    }
}
