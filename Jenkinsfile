pipeline {
    agent any
    properties([parameters([gitParameter(branch: '', branchFilter: '.*', defaultValue: '0.0.5', description: 'tags for your application', name: 'tag', quickFilterEnabled: false, selectedValue: 'NONE', sortMode: 'NONE', tagFilter: '*', type: 'PT_TAG')])])
      git(name:
    tools {
        maven 'maven-3'
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
                          file: 'target/myweb-0.0.5.war', 
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
