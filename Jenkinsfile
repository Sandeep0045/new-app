pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
         stage('Build'){
             steps{
                  sh script: 'mvn clean package'
             }
         }
         stage('Deploy to Nexus'){
             steps{
                  nexusArtifactUploader artifacts: [
                      [
                          artifactId: 'myweb', 
                          classifier: '', 
                          file: 'target/my-app-0.0.5.war', 
                          type: 'war'
                    ]
                 ], 
                 credentialsId: 'nexus3', 
                 groupId: 'in.javahome', 
                 nexusUrl: '172.31.77.32:8081', 
                 nexusVersion: 'nexus3', 
                 protocol: 'http', 
                 repository: 'tomcat-release-app', 
                 version: '0.0.5'
     }
   }
 } 
}    
