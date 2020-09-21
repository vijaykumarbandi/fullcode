node {
def mvn = tool (maven : 'M2-HOME', type: 'maven') + '/bin/mvn'
stage('compile stage') {
sh "${mvn} compile"
}
stage('package stage') {
sh "${mvn} package"
}
stage('sonarqube analysis') {
withSonarQubeEnv('sonarqube') {
sh "${mvn} sonar:sonar"
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












