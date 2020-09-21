node{
   stage('SCM Checkout'){
     git 'https://github.com/vijaykumarbandi/fullcode.git'
   }
   stage('Compile'){
      def mvnHome =  tool name: 'M2-HOME', type: 'maven'   
      sh "${mvnHome}/bin/mvn compile"
   }
  stage('Package'){
      def mvnHome =  tool name: 'M2-HOME', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
  stage('SonarQube Analysis'){
        def mvnHome =  tool name: 'M2-HOME', type: 'maven'
        withSonarQubeEnv('sonarqube') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
stage('Nexusartifact uploader'){
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
