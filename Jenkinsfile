pipeline {
    agent any
    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=/root/.m2"
    }

    stages {
        stage('Build & Test') {
            agent {
                docker {
                    image 'maven:3.9.13-eclipse-temurin-17'
                    args "" // Không mount workspace từ host
                }
            }
            steps {
                // Clone repo trực tiếp trong container
                sh 'git clone -b main https://github.com/NguyenTanThanh0709/cicd.git /app'
                dir('/app') {
                    sh 'java -version'
                    sh 'mvn -version'
                    sh 'mvn clean package' // build + test
                }
            }
        }
    }
}