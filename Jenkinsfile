pipeline {
    agent any
    tools {
        maven 'M3'
    }
    stages {
        stage('SonarQube') {
            steps {
                withSonarQubeEnv("My SonarQube Server") {
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=devops-demo -Dsonar.sources=src -Dsonar.language=java -Dsonar.java.binaries=."
                }
            }
        }
        stage("Quality Gate"){
            steps {
                script {
                  timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
                    def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                    if (qg.status != 'OK') {
                        def committerEmail = sh (
                              script: 'git --no-pager show -s --format=\'%ae\'',
                              returnStdout: true
                        ).trim()
                        mail bcc: '', body: 'Build failed!.', cc: 'santaduda@gmail.com', from: '', replyTo: '', subject: 'Quality Gate failed', to: "${committerEmail}"
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      
                    }
                  }
                }
            }
        }
        stage('Build') {
            steps {
                echo "Build completed"    
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy completed"    
            }
        }
    }
} 
