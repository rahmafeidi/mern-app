pipeline {
  agent any
  
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t rahmafeidi/api api/'
        sh 'docker build -t rahmafeidi/ui ui/'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push rahmafeidi/api'
        sh 'docker push rahmafeidi/ui'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
