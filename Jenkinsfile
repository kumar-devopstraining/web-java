node{
   stage('SCM Checkout'){
     git branch:'main',url:'https://github.com/kumar-devopstraining/web-java'
   }
   stage('Build'){
      // declaring maven home path
      def mvnHome =  tool name: 'maven3', type: 'maven'
      sh "${mvnHome}/bin/mvn package"
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
           file: 'target/chatting.war', 
           type: 'war'
          ]
       ],
         credentialsId: 'nexus-login',
         groupId: 'whatsapp',
         nexusUrl: 'http://3.210.184.10:8081',
         nexusVersion: 'nexus3',
         protocol: 'http', 
         repository: 'maven-releases', 
         version: '1.0.0'
   } 

   
   stage('deploy to QA'){
     sshagent(['tomcat login']) {
       sh 'scp -o StrictHostKeyChecking=no target/chatting.war tomcat@172.31.79.5:/opt/tomcat/apache-tomcat/webapps/'
}
   }
}

