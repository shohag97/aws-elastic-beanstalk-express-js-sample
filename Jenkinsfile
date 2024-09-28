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
                        sh 'npm install --save > logs/dependencies.log 2>&1'
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
                        sh 'npm run build > logs/build.log 2>&1'
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
                        sh 'npm test > logs/test.log 2>&1'
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
                withCredentials([string(credentialsId: 'snyk-token', variable: 'SNYK_TOKEN')]) {
                    script {
                        try {
                            echo 'Running Snyk Security Scan...'
                            sh 'npm install snyk > logs/snyk-install.log 2>&1'
                            sh './node_modules/.bin/snyk test > logs/snyk-scan.log 2>&1 || true'
                            echo 'Snyk security scan completed.'
                        } catch (Exception e) {
                            echo 'Snyk security scan failed.'
                            error('Stopping pipeline due to failure in Security Scan stage.')
                        }
                    }
                }
            }
        }
    }
}
