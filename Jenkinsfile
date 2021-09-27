pipeline {
  agent any
  environment {
    API_ENTITY_ID='6151a8a2170ca3006f05e4e7' 
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
        sh "curl -X PUT --url 'https://www.apimatic.io/api/api-entities/${env.API_ENTITY_ID}' -v --basic --user ${env.USERNAME}:${env.PASSWORD} -H 'content-type:multipart/form-data' -H 'Accept:application/zip' -F 'file=@Specs/portal-input.zip'"
      }
    }
    stage('Publish Portal') {
      steps {
        sh "curl --location --request PUT -v --basic --user ${env.USERNAME}:${env.PASSWORD} --url 'https://www.apimatic.io/api/api-entities/${env.API_ENTITY_ID}/portal/publish' -H 'Content-Length:0'  -H 'content-type:multipart/form-data'"
      }
    }
  }
}
