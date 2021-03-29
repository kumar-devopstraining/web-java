node{
   stage('SCM Checkout'){
     git branch:'main',url:'https://github.com/kumar-devopstraining/web-java'
   }
   stage('Build'){
      // declaring maven home path
      def mvnHome =  tool name: 'maven', type: 'maven'  
      sh "${mvnHome}/bin/mvn package"
   }
   
   // stage('SonarQube Analysis') {
      //  def mvnHome =  tool name: 'maven', type: 'maven'
       // withSonarQubeEnv('sonar1') { 
         // sh "${mvnHome}/bin/mvn sonar:sonar"
        //}
    //}
   stage('deploy to QA'){
      sshagent(['tomcat']) {
       sh 'scp -o StrictHostKeyChecking=no target/chatting.war tomcat@172.31.43.14:/opt/tomcat/tomcat7/webapps/'
}
   }
}
