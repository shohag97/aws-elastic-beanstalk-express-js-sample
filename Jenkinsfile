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
    }
}
