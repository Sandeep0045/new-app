pipeline {
    agent any
    parameters {
         gitParameter name: 'tag'
                      type: 'Tag'
                      defaultValue: '0.0.5'
    }    
    tools {
        maven 'maven-3'
    }
    stages{
         stage('scm checout')
             echo "taking git tag from repo ${params.tag}"
             git url: 'https://github.com/Sandeep0045/new-app.git', tag: "${params.tag}"
              }
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

