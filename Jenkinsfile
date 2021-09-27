pipeline {
  agent any
  environment {
    API_ENTITY_ID='613b5f7b3300989c5dc09ffe' 
  }
  stages {
    stage('validate') {
      steps {
        sh "curl --version"
      }
    }
    stage('install zip'){
      steps {
        sh 'sudo apt-get install zip unzip'
      }
    }
    stage('zip input files') {
      steps {
        dir('./Specs') {
          sh 'zip -r portal-input.zip *'
        }
      }
    }
    stage('list') {
      steps {
        dir('./Specs') {
          sh 'zip -sf portal-input.zip'
        }
      }
    }
  }
}
