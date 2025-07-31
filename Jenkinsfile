pipeline {
    agent any

    stages {
        stage('Tester Docker') {
            steps {
                sh 'docker --version'
                sh 'docker ps'
            }
        }

        stage('Construire l\'image') {
            steps {
                sh 'docker build -t crud-app:latest .'
            }
        }

        stage('Déployer l\'application') {
            steps {
                sh '''
                    docker stop crud-app || true
                    docker rm crud-app || true
                    docker run -d --name crud-app -p 8081:80 \
                    -v /var/www/html/database.sqlite:/var/www/html/database.sqlite \
                    crud-app:latest
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



        




