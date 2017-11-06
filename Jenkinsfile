pipeline{
     agent any
     
     tools{
maven 'M3_HOME'
jdk 'JAVA_HOME'
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
