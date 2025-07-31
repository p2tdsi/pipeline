pipeline {
    agent any  // ← utilise l'agent Jenkins "classique", sur l'hôte

    stages {
        stage('Test Docker') {
            steps {
                sh 'docker --version'
                sh 'docker ps'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t crud-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop crud-app || true
                    docker rm crud-app || true
                    docker run -d --name crud-app -p 8081:80 -v /var/www/html:/usr/share/nginx/html crud-app:latest
                '''
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


        




