pipeline{

  agent any
  stages{
  
      stage ('Build'){

      sh 'mvn clean package'

      post{
         sucesss{
	       
               echo 'Now Archiving!!!'
               archiveArtifacts artifacts: '**/target/*.war'
                } 
          }
 
      }
   

 }


}
