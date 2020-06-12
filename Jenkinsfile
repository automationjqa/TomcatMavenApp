pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/annajel/TomcatMavenApp.git', branch: 'master')
      }
    }

    stage('deploy') {
      steps {
        sh 'mvn clean package jelastic:deploy'
      }
    }

    stage('archival') {
      steps {
        archiveArtifacts 'target/*.war'
      }
    }

    stage('notify') {
      steps {
        emailext(subject: '"${status}: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\'"', body: '"""<p>${status}: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\':</p>         <p>Check console output at <a href=\'${env.BUILD_URL}\'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>"""', attachLog: true, to: 'ash@gmail.com')
      }
    }

  }
  environment {
    env = 'blueOcean'
  }
}