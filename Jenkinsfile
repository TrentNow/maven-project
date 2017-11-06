pipeline {
     
     tools{
          maven 'M3'
          jdk 'JAVA_HOME'
     }
     
     agent any
     stages{
          stage('Initialize'){
               steps{
                    sh """
                    echo 'M3_HOME =${M3_HOME}'
                    echo 'PATH = ${PATH}'
                    """
               }
          
          }
          stage('Build'){
               steps{
                    sh 'mvn clean package'
               }
               post{
                    success{
                         echo 'Archiving artifacts!!!'
                         archiveArtifacts artifacts: '**/target/*.war'
                    }
               
               }
          
          }
          stage('Deploy to staging'){
               steps{
                    build job: deploy-to-staging
               
               }
                                           
           }
         
     }
}
