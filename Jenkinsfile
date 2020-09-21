pipeline {
agent any
tools {
maven 'M2-HOME'
}
stages {
stage('compile stage') {
steps {
sh script: 'clean compile'
}
}
stage('package stage') {
steps {
sh script: 'package'
}
}
stage('sonarqube analysis') {
steps {
withSonarQubeEnv('sonarqube') {
sh script: 'sonar:sonar'
}
}
}
stage('nexus artifact uploader') {
steps {
script {
nexusArtifactUploader  artifacts: [
[
artifactId: 'fullcode',
classifier: '',
file: "/target/fullcode-1.0.0-SNAPSHOT.war",
type: 'war'
]
],
credentialsId: 'nexus',
groupId: 'in.javahome',
nexusUrl: '192.168.33.10:8081',
nexusVersion: 'nexus3',
repository: 'kumar',
protocal: 'http',
version: '1.0.0'
}
}
}
}
}











