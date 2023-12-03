pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Paso para clonar el repositorio
                checkout scm
                /*
                En un Declarative Pipeline, checkout scm es una abstracción que maneja automáticamente los detalles de cómo se debe realizar la clonación para el origen del código fuente definido en la configuración del trabajo.

                Por lo tanto, si estás utilizando un Declarative Pipeline y la configuración del origen del código fuente (SCM) ya está definida en Jenkins, no necesitas agregar nada más. Si estás escribiendo un Scripted Pipeline y necesitas ajustes más detallados, podrías considerar la sintaxis que mencionaste.
                Sin embargo, para la mayoría de los casos, checkout scm en un Declarative Pipeline es suficiente y manejará automáticamente los detalles de Git.
                */
            }
        }

        stage('Build') {
            steps {
                // Paso para construir el proyecto con Maven
                script {
                    def mvnHome = tool 'maven-tool' // Asegúrate de tener una instalación de Maven en Jenkins llamada 'Maven'
                    sh "${mvnHome}/bin/mvn clean install"
                }
            }
        }

        stage('Unit Tests') {
            steps {
                // Paso para ejecutar las pruebas
                script {
                    def mvnHome = tool 'maven-tool'
                    sh "${mvnHome}/bin/mvn test"
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Paso para realizar el análisis estático de código con SonarQube
                script {
                    def scannerHome = tool 'sonar-scanner'
                    withSonarQubeEnv('sonarqube') {
                         sh "${scannerHome}/bin/sonar-scanner
                          -Dsonar.projectKey=tpcurso"
                    }
                }
            }
        }

    }

    post {
        success {
            // Acciones adicionales si el pipeline tiene éxito
             echo '¡Pipeline completado con éxito!'
        }
    }
}
