node{
   stage('SCM Checkout'){
     git branch:'main',url:'https://github.com/kumar-devopstraining/web-java'
   }
   stage('Build'){
      // declaring maven home path
      def mvnHome =  tool name: 'maven3', type: 'maven'
      sh "${mvnHome}/bin/mvn clean package"
   }
   
   // stage('SonarQube Analysis') {
      // def mvnHome =  tool name: 'maven', type: 'maven'
       // withSonarQubeEnv('sonar1') { 
         // sh "${mvnHome}/bin/mvn sonar:sonar"
        //}
    //}
  stage('nexus upload') {
   nexusArtifactUploader artifacts: [
         [
            artifactId: 'chatting', 
           classifier: '', 
           file: 'target/chatting-2.0.0-SNAPSHOT.war', 
           type: 'war'
          ]
       ],
         credentialsId: 'nexus-login',
         groupId: 'whatsapp',
         nexusUrl: '3.226.251.23:8081',
         nexusVersion: 'nexus3',
         protocol: 'http', 
         repository: 'mysnapshot', 
         version: '2.0.0-SNAPSHOT'
   } 

   
   stage('deploy to QA'){
     sshagent(['tomcat login']) {
       sh 'scp -o StrictHostKeyChecking=no target/*.war tomcat@172.31.79.5:/opt/tomcat/apache-tomcat/webapps/'
}
   }
}

