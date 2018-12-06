pipeline {
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
	post {
        always {
            archiveArtifacts artifacts: 'target/hello.jar.jar', onlyIfSuccessful: true
        }
    }
}