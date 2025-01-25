pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                deleteDir() // Limpia el workspace antes de hacer checkout
                checkout scm // Realiza el checkout del código
            }
        }

        stage('Build') {
            steps {
                // Ejecuta el comando de construcción; ajusta según tu herramienta
                sh 'mvn -f first-api-rest clean install' // Para un proyecto Maven
                // bat 'mvn clean install' // Usar bat si estás en un entorno Windows
            }
        }

        stage('Test') {
            steps {
                // Ejecuta el comando de pruebas; ajusta según tu herramienta
                sh 'mvn -f first-api-rest test' // Para un proyecto Maven
                // bat 'mvn test' // Usar bat si estás en un entorno Windows
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