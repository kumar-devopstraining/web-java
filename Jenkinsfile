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
         nexusUrl: '172.31.77.152:8081',
         nexusVersion: 'nexus2',
         protocol: 'http', 
         repository: 'http://18.207.252.91:8081/repository/maven-releases/', 
         version: '1.0.0'
   }
}
   
   //stage('deploy to QA'){
    //  sshagent(['tomcat']) {
      // sh 'scp -o StrictHostKeyChecking=no target/chatting.war tomcat@172.31.43.14:/opt/tomcat/tomcat7/webapps/'
//}
   //}

