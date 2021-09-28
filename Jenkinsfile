pipeline {
  agent any
  environment {
    API_ENTITY_ID='6152d8fd0a2e976237f59ad8' 
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
        sh "curl -X PUT --url 'https://dev.apimatic.io/api/api-entities/${env.API_ENTITY_ID}' -v --basic --user ${env.USERNAME}:${env.PASSWORD} -H 'Content-Type: multipart/form-data' -H 'Accept: application/zip' -F 'file=@Specs/portal-input.zip'"
      }
    }
    stage('Publish Portal') {
      steps {
        sh "curl -X PUT -v --basic --user ${env.USERNAME}:${env.PASSWORD} --url 'https://dev.apimatic.io/api/api-entities/${env.API_ENTITY_ID}/portal/publish' -H 'Content-Length: 0' -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Accept-Encoding: gzip,deflate,br'"
      }
    }
  }
}
