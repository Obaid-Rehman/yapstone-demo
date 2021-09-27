pipeline {
  agent any
  environment {
    API_ENTITY_ID='613b5f7b3300989c5dc09ffe' 
    USERNAME='obaid.khattak@apimatic.io'
    PASSWORD='Bigdaddy.123'
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
          zip zipFile:'input-portal.zip', overwrite: true
        }
      }
    }
    stage('Inplace Import') {
      steps {
        sh "curl -X PUT --url 'https://www.apimatic.io/api/api-entities/${env.API_ENTITY_ID}' -H 'content-type:multipart/form-data' -H 'Authorization:${{ secrets.CREDENTIALS }}' -F 'file=@Specs/portal-input.zip'"
      }
    }
  }
}
