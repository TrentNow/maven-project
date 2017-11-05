pipeline{

  agent any
  stages{
  
      stage('Build'){
          steps{
             
              withMaven(
        // Maven installation declared in the Jenkins "Global Tool Configuration"
        maven: 'M2',
        // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
        // Maven settings and global settings can also be defined in Jenkins Global Tools Configuration
        mavenSettingsConfig: 'my-maven-settings',
        mavenLocalRepo: '.repository') {
 
      // Run the maven build
      sh "mvn clean install"
             
          }

          post{
              success{
	          echo 'Now Archiving!!!'
                  archiveArtifacts artifacts: '**/target/*.war'
                } 
          }
 
      }
   

 }


}
