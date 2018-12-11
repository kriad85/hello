pipeline {
    environment {
       registry = "localhost:5000/hello"
       dockerImage = ''
    }
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /home/karim/cloudformation:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn install' 
            }
        }
    }
	stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + “:$BUILD_NUMBER”
        }
      }
    }
	stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', '' ) {
            dockerImage.push()
          }
        }
      }
    }
	post {
        always {
            archiveArtifacts artifacts: 'target/hello.jar.jar', onlyIfSuccessful: true
        }
    }
}