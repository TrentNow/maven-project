pipeline{
   agent any
   
   tools{
      maven 'M3'
      jdk 'JAVA_HOME'
   }
   parameters{
      string(name: 'tomcat-dev', defaultValue: '34.231.241.89', description: 'Staging server')
      string(name: 'tomcat-prod', defaultValue: '34.206.64.59', description: 'Production server')
   }
   triggers{
      pollSCM('* * * * *')
   }
   stages{
      stage('Initialize'){
         steps{
         sh '''
         echo "M3_HOME =${M3_HOME}"
         echo "PATH = ${PATH}"
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
      stage('Deployment'){
         parallel{
            stage('Deploy to staging'){
               steps{
                  sh "scp -i /home/ec2-user/Cloud_KP.pem **/target/*.war ec2-user@${params.tomcat-dev}:/home/ec2-user/tomcat/webapps"
               }
            }
            stage('Deploy to production'){
               steps{
                  sh "scp -i /home/ec2-user/Cloud_KP.pem **/target/*.war ec2-user@${params.tomcat-prod}:/home/ec2-user/tomcat/webapps"
               }
            }
         }
      }
   }

}
