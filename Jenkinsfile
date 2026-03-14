pipeline {
    agent any
    environment {
        MAVEN_OPTS = '-Dmaven.repo.local=/root/.m2/repository'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/NguyenTanThanh0709/cicd.git'
            }
        }
        stage('Build & Test') {
            agent {
                docker {
                    image 'maven:3.9.13-eclipse-temurin-17'
                    args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                sh 'java -version'
                sh 'mvn -version'
                sh 'mvn clean package -DskipTests'  // chạy luôn unit test
                sh 'mvn test'
            }
        }

    }
}