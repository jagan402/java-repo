pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            credentialsId: 'mygit',
            url: 'https://github.com/jagan402/java-repo.git'
      }
    }

    stage('Build') {
      steps { echo 'Building...' }
    }

    stage('Test') {
      steps { echo 'Running tests...' }
    }
  }

  post {
    success { echo 'Pipeline completed successfully.' }
    failure { echo 'Pipeline failed.' }
  }
}
