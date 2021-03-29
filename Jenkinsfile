node{
   stage('SCM Checkout'){
     git branch: 'main' url: 'https://github.com/kumar-devopstraining/web-java'
   }
   stage('Build'){
      // declaring maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven-3', type: 'maven'
        withSonarQubeEnv('sonar1') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
