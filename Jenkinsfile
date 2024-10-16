pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JDK8'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('FrancisGo67890/cloudfreak', "./docker")

                 // Tag the image with version 3
                 sh "docker tag francisgo67890/cloudfreak:latest registry.hub.docker.com/FrancisGo67890/cloudfreak:3"
                 // Push the tagged image
                 sh "docker push registry.hub.docker.com/FrancisGo67890/cloudfreak:3"
                 
           }
        }
	  }
    }
}
