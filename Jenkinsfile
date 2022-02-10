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
	    stage('sonarqube analysis') {
		     steps{
			      withsonarqubeEnv('sonarqube 8.9.7') {
				  sh "mvn sonar:sonar"
				  }
			}	  
	  }
	  }
	  }
