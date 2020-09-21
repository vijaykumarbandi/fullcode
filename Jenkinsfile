pipeline {
    agent any
    tools {
        maven 'M2-HOME'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        
stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'M2-HOME', type: 'maven'
        withSonarQubeEnv('sonarqube') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
stage('Upload War To Nexus'){
            steps{
                script{  
                   nexusArtifactUploader artifacts: [
                       [
                            artifactId: 'fullcode',
                            classifier: '',
                            file: "target/fullcode-1.0.0-SNAPSHOT.war",
                            type: 'war'
                           ]
                       ],
                    credentialsId: 'nexus3',
                    groupId: 'in.javahome',
                    nexusUrl: '192.168.33.10:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'kumar',
                    version: '1.0.0'
              }
            }
        }
    }
