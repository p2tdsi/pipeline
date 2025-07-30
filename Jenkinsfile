pipeline {
    agent {
        docker {
            image 'docker:20.10' // image officielle avec docker CLI
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

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
                    docker run -d --name crud-app -p 8081:80 -v /var/www/html/database.sqlite:/var/www/html/database.sqlite crud-app:latest
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

        




