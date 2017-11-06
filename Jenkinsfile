pipeline{
   
   agent any
   tools{
      maven: 'M3'
      jdk: 'JAVA_HOME'
   }
   stages{
      stage('Initialize'){
         steps{
            sh '''
            echo "PATH = ${PATH}"
            echo "M3_HOME = ${M3_HOME}"
            '''
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
            build job: 'deploy-to-staging'
         
         }
      
      }
      stage('Deploy to Production'){
         steps{
            timeout(time: 5, unit: 'DAYS'){
               input message: 'Would you like to deploy to production?'
            
            }
         build job: 'deploy-to-prod'
         
         }
         
         post{
            success{
               echo 'Build deployed successfully'
            
            }
            failure{
               echo 'build can not be deployed'
            
            
            }
            
         
         }
      
      }
   }

}
