pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                deleteDir()
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -f first-api-rest clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -f first-api-rest test'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}