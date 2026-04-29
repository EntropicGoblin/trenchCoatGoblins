pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = 'trenchcoatgoblins'
        POSTGRES_USER = 'tcg'
        POSTGRES_DB = 'tcg'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Inject Secrets') {
            steps {
                withCredentials([string(credentialsId: 'tcg-postgres-password', variable: 'PG_PWD')]) {
                    sh '''
                        mkdir -p secrets
                        printf '%s' "$PG_PWD" > secrets/postgres_password.txt
                        chmod 600 secrets/postgres_password.txt
                    '''
                }
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker-compose build --no-cache'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
            }
        }

        stage('Cleanup') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }

    post {
        always {
            sh 'rm -f secrets/postgres_password.txt'
        }
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
            sh 'docker-compose logs'
        }
    }
}
