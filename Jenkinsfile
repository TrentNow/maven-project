pipeline{
     agent any
     stages{
          stage('Build'){
              steps{
              sh 'mvn clean package'
             }
              post{
                 success{
                       echo 'Storing archive!!!'
                       archiveArtifacts artifacts: '**/target/*.war'
                 
                 }
              
              }
          
          
          } 
     
     
     
     
     
     
     
     
     }

}
