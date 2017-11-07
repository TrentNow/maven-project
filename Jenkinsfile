pipeline{
   agent any
   
   tools{
      maven 'M3'
      jdk 'JAVA_HOME'
   }
   parameters{
      string(name: 'tomcatdev', defaultValue: '34.205.50.2', description: 'Staging server')
      string(name: 'tomcatprod', defaultValue: '34.238.28.142', description: 'Production server')
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
                  sh 'scp -i /home/ec2-user/Cloud_KP.pem **/target/*.war ec2-user@${params.tomcatdev}:/home/ec2-user/tomcat/webapps'
               }
            }
            stage('Deploy to production'){
               steps{
                  sh 'scp -i /home/ec2-user/Cloud_KP.pem **/target/*.war ec2-user@${params.tomcatprod}:/home/ec2-user/tomcat/webapps'
               }
            }
         }
      }
   }

}
