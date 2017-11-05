pipeline{

  agent any
  stages{
  
      stage('Build'){
          steps{
            def mvnHome = tool 'M2_HOME'
            env.PATH = "${mvnHome}/bin:${env.PATH}"
            sh 'mvn clean package'
             
          }

          post{
              success{
	          echo 'Now Archiving!!!'
                  archiveArtifacts artifacts: '**/target/*.war'
                } 
          }
 
      }
   

 }


}
