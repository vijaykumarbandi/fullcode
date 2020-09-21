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
artifactId: '',
classifier: '',
file: "",
type: ''
]
],
credentialsId: '',
groupId: '',
nexusUrl: '',
nexusVersion: '',
repository: '',
protocal: '',
version: ''
}
}
}
}
}











