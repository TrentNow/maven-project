pipeline{
     agent any
     
     tools{
maven 'maven 3'
jdk 'java 8'
}
     
     
     stages{
          
          stage ("initialize") {
               steps {
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
                       echo 'Storing archive!!!'
                       archiveArtifacts artifacts: '**/target/*.war'
                 
                 }
              
              }
          
          
          } 
     
     
     
     
     
     
     
     
     }

}
