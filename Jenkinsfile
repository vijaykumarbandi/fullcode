pipeline {
    agent any
    tools {
        maven 'M2-HOME'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
     stages {
    stage('SonarQube Analytics') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh script:'mvn sonar:sonar'
                }
            }
        }
   
        stage('Build') {
            steps {
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload War To Nexus') {
            steps {
                script {  
                   nexusArtifactUploader artifacts: [
                       [
                            artifactId: 'fullcode',
                            classifier: '',
                            file: "target/fullcode-2.0.0-SNAPSHOT.war",
                            type: 'war'
                           ]
                       ],
                    credentialsId: 'nexus',
                    groupId: 'in.javahome',
                    nexusUrl: '192.168.33.10:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'kumar',
                    version: '2.0.0'
              }
            }
        }
    stage('email notification') {
   steps {
       script {
    mail bcc: '', body: '''hi 
its successful''', cc: '', from: '', replyTo: '', subject: 'Jenkins test file', to: 'vijaykumarbandi6594@gmail.com'
   }
  }
}
     }
}

    

