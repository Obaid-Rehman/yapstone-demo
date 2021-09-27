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
    stage('Zip files'){
      steps {
        dir('./Specs') {
          zip zipFile:'input-portal.zip'
        }
      }
    }
  }
}
