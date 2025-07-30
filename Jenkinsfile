pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'crud-app:latest'
        CONTAINER_NAME = 'crud-app'
        HOST_PORT = '8081'
        CONTAINER_PORT = '80'
        SQLITE_VOLUME = '/var/www/html/database.sqlite:/var/www/html/database.sqlite'
    }

    stages {

        stage('Test Docker') {
            steps {
                echo '🔍 Vérification de Docker'
                sh 'docker --version'
                sh 'docker ps'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "🛠️ Construction de l’image Docker ${DOCKER_IMAGE}"
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Déploiement du conteneur ${DOCKER_IMAGE}"

                // Arrêt et suppression si le conteneur existe
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"

                // Lancement du conteneur
                sh """
                    docker run -d --name ${CONTAINER_NAME} \
                    -p ${HOST_PORT}:${CONTAINER_PORT} \
                    -v ${SQLITE_VOLUME} \
                    ${DOCKER_IMAGE}
                """
            }
        }
    }

    post {
        failure {
            echo '❌ Échec du pipeline. Vérifiez les logs.'
        }
        success {
            echo '✅ Déploiement terminé avec succès.'
        }
    }
}




