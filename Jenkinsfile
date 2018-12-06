pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/home/karim' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn install' 
            }
        }
    }
}