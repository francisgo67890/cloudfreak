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
                 def customImage = docker.build('francisgo67890/petclinic', "./docker")
                 docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                 sh "docker tag francisgo67890/cloudfreak:latest registry.hub.docker.com/francis579/petclinic:3"
                 sh "docker push registry.hub.docker.com/francis579/petclinic:3"

                 }   
            
     
           }
        }
	  }
    }
}
