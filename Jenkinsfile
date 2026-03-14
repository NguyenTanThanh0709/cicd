pipeline {
    agent {
        docker {
            image 'maven:3.9.13-eclipse-temurin-17'
            args '-v /root/.m2:/root/.m2'
        }
    }

    stages {
        stage('Check Java & Maven') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }
    }
}