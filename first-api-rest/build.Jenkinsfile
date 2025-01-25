pipeline {
    agent any

    triggers {
        // Este bloque es opcional si usas webhooks, pero puede ser útil en caso de polling
        pollSCM('H/5 * * * *') // Verifica cambios cada 5 minutos (opcional)
    }

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
                sh 'mvn clean install' // Para un proyecto Maven
                // bat 'mvn clean install' // Usar bat si estás en un entorno Windows
            }
        }

        stage('Test') {
            steps {
                // Ejecuta el comando de pruebas; ajusta según tu herramienta
                sh 'mvn test' // Para un proyecto Maven
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