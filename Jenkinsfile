pipeline {
  agent any
  environment {
    API_ENTITY_ID='613b5f7b3300989c5dc09ffe' 
    USERNAME='obaid.khattak@apimatic.io'
    PASSWORD='Bigdaddy.123'
  }
  stages {
    stage('Validate') {
      steps {
        sh "curl --version"
      }
    }
    stage('Zip Files'){
      steps {
        dir('./Specs') {
          zip zipFile:'portal-input.zip', overwrite: true
        }
      }
    }
    stage('Inplace Import') {
      steps {
        sh "curl -X PUT --url 'https://www.apimatic.io/api/api-entities/${env.API_ENTITY_ID}' --user ${env.USERNAME}:${env.PASSWORD} -H 'content-type:multipart/form-data' -F 'file=@Specs/portal-input.zip'"
      }
    }
    stage('Publish Portal') {
      steps {
        sh "curl --location --request PUT --user ${env.USERNAME}:${env.PASSWORD} --url 'https://www.apimatic.io/api/api-entities/${env.API_ENTITY_ID}/portal/publish' -H 'Content-Length:0'"
      }
    }
  }
}
