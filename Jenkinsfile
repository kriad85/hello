pipeline {
    environment {
       registry = "localhost:5000/hello"
       dockerImage = ''
    }
	agent none
    stages {
        stage('Build') { 
		    agent {
               docker {
                  image 'maven:3-alpine' 
                  args '-v /home/karim/cloudformation:/root/.m2' 
               }
            }
            steps {
                sh 'mvn install' 
            }
			post {
              always {
                archiveArtifacts artifacts: 'target/hello.jar.jar', onlyIfSuccessful: true
              }
            }
        }
	    stage('Building image') {
		    agent any
            steps{
              script {
                 dockerImage = docker.build registry + ":$BUILD_NUMBER"
              }
		    }
        }
	    stage('Deploy Image') {
	        agent any
            steps{
              script {
                 docker.withRegistry( '', '' ) {
                    dockerImage.push()
                 }
             }
            }
        }
	}   
}