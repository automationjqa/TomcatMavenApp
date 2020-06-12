pipeline {
  agent any
  
  checkout scm
  
  stages {
    stage('deploy') {
      withMaven(maven: 'maven'){
            sh label: '', script: 'mvn clean package jelastic:deploy'
            }
      }

      stage('notify') {
        steps {
          emailext(subject: '"${status}: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\'"', body: '"""<p>${status}: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\':</p>         <p>Check console output at <a href=\'${env.BUILD_URL}\'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>"""', attachLog: true, to: 'ash@gmail.com')
        }
      }
    }
 }
  
    environment {
      env = 'blueOcean'
    }
  }
