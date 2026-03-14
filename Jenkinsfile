pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_REPO = 'nguyentanthanh0709/testing-spring-boot-app'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3.9.13-eclipse-temurin-17'
                }
            }

            steps {
                sh 'java -version'
                sh 'mvn -version'
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                    docker build -t $DOCKER_REPO:$IMAGE_TAG .
                    docker tag $DOCKER_REPO:$IMAGE_TAG $DOCKER_REPO:latest
                """
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push $DOCKER_REPO:$IMAGE_TAG
                        docker push $DOCKER_REPO:latest
                    """
                }
            }
        }


    }
}