pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-id')
        DOCKER_IMAGE = 'first-api-rest-f'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                deleteDir()
                checkout scm
                echo "Tag: ${env.GIT_REF}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS.password} | docker login -u ${DOCKERHUB_CREDENTIALS.username} --password-stdin"
                    sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
    }
}