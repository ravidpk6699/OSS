pipeline {
    agent any
  tools {
    maven 'maven3'
	}
	stages{
	    stage('Build') {
		  steps{
		      sh 'mvn clean package'
      }
      }
	  stage('upload war to nexus'){
          steps{	  
	         nexusArtifactUploader artifacts: [
	  [
	    artifactId: 'WebApp', 
		classifier: '', 
		file: 'target/WebApp-1.1.0.war', 
		type: 'war'
		]
		], 
		credentialsId: 'nexus3', 
		groupId: 'Demoapp', 
		nexusUrl: '20.212.18.14:8081', 
		nexusVersion: 'nexus3', 
		protocol: 'http', 
		repository: 'project-oss', 
		version: '1.1.0'
	  }
	  }
	  }
	  }
