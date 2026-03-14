pipeline {
    agent any
    environment {
        MAVEN_OPTS = '-Dmaven.repo.local=/root/.m2/repository'
    }

    stages {
        stage('Check Java & Maven') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }

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
                sh 'mvn clean test'  // chạy luôn unit test
                sh 'mvn package'     // build jar
            }
        }

    }
}