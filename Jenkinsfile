
pipeline {
    agent any

    stages {

        stage('Validar codigo') {
            steps {
                echo 'Codigo descargado de GitHub'
            }
        }

        stage('Compilar Java') {
            steps {
                bat '''
                    if not exist dist mkdir dist
                    javac -d dist src\\Main.java
                '''
            }
        }

        stage('Generar binario') {
            steps {
                bat '''
                    jar cfe aplicacion.jar Main -C dist .
                '''
            }
        }

        stage('Probar aplicacion') {
            steps {
                bat '''
                    java -jar aplicacion.jar
                '''
            }
        }

        stage('Publicar artefacto') {
            steps {
                archiveArtifacts artifacts: 'aplicacion.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESS - Binario generado'
        }

        failure {
            echo 'BUILD FAILED - Revisar logs'
        }
    }
}
