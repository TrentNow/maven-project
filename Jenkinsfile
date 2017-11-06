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
          stage('Deploy to production'){
               steps{
                    timeout(time: 5, unit: 'DAYS' ){
                         input message: 'Can this build be deployed to production?'
                    }
               build job: deploy-to-prod      
              }
          
               post{
                    success{

                         echo 'Build being deployed'
                    }
                    failure{
                         echo 'Build cant be deployed at this moment'
                    
                    }
               }
          }
     }
}
