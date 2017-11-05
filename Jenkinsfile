pipeline{

  agent any
  stages{
  
      stage('Build'){
          steps{
              sh 'mvn clean package'
          }

          post{
              sucess{
	          echo 'Now Archiving!!!'
                  archiveArtifacts artifacts: '**/target/*.war'
                } 
          }
 
      }
   

 }


}
