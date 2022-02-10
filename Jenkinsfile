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
			      withSonarQubeEnv('sonarqube 8.9.7') {
				  sh "mvn sonar:sonar"
				  }
			}
		}
		stage("Quality Gate") {
		steps {
		timeout(time:1, unit: 'HOURS') {
		waitForQualityGate abortPipeline: true
		}
		}
	  }
	  }
	  }
	  
