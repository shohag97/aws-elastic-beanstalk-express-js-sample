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
