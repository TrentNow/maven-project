pipeline{

  agent any
  stages{
  
      stage('Build'){
          steps{
              sh 'echo $PATH'
              sh 'echo $M2'
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
