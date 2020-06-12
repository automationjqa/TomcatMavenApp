node {
    checkout scm
    notify('Started')
    try {               
        stage('deploy') {
            withMaven(maven: 'maven'){
            sh label: '', script: 'mvn clean package jelastic:deploy'
            }
        }
        
        stage('archival') {
            archiveArtifacts 'target/*.war'
        }
        
        notify('Success')
        
    } catch (err) {
        notify("Error ${err}")
        echo "Caught: ${err}"
        currentBuild.result = 'FAILURE'
    }
}

def notify(status){
    emailext (
      to: "ash@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}


