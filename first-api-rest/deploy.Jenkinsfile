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
                sh 'ls -la' // Verifica que el Dockerfile esté presente
                echo "Tag: ${env.GIT_REF}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    try {
                        sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                    } catch (Exception e) {
                        echo "Build failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Stopping the build due to previous error.")
                    }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    try {
                        sh "echo ${DOCKERHUB_CREDENTIALS.password} | docker login -u ${DOCKERHUB_CREDENTIALS.username} --password-stdin"
                        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    } catch (Exception e) {
                        echo "Docker push failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Stopping the build due to previous error.")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Image pushed to Docker Hub successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}