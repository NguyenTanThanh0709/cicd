pipeline {
    agent any
    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=$WORKSPACE/.m2"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/NguyenTanThanh0709/cicd.git'
            }
        }
        stage('Prepare Maven Repo') {
            steps {
                sh 'mkdir -p $WORKSPACE/.m2'
                sh 'chmod -R 777 $WORKSPACE/.m2'
            }
        }
        stage('Build & Test') {
            agent {
                docker {
                    image 'maven:3.9.13-eclipse-temurin-17'
                    args "-v ${env.WORKSPACE}/.m2:/root/.m2 -v ${env.WORKSPACE}:/app"
                }
            }
            steps {
                dir('/app') {
                    sh 'mvn clean package'
                }
            }

        }

    }
}