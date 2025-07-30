pipeline {
    agent any

    stages {
        // Nettoyage du workspace pour éviter les erreurs liées au répertoire
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

      

        // Déploiement du conteneur Docker avec l'image existante
        stage('Deploy') {
            steps {
                sh 'docker stop crud-app || true'
                sh 'docker rm crud-app || true'
                sh 'docker run -d --name crud-app -p 8081:80 -v /var/www/html/database.sqlite:/var/www/html/database.sqlite crud-app:latest'
            }
        }
    }

    // Gestion des résultats
    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            echo 'Échec du pipeline. Vérifiez les logs.'
        }
    }
}



