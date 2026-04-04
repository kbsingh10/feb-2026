pipeline {
    agent any

    environment {
        APP_NAME = "feb-2026-app"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main',
                    url: 'https://github.com/kbsingh10/feb-2026.git',
                    credentialsId: 'git-cred01'
            }
        }

        stage('Check Files') {
            steps {
                echo 'Listing files...'
                sh 'ls -ltr'
            }
        }

        stage('Docker Check') {
            steps {
                echo 'Checking Docker...'
                sh 'docker ps'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh '''
                    docker build -t $APP_NAME .
                '''
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running container...'
                sh '''
                    docker stop $APP_NAME || true
                    docker rm $APP_NAME || true
                    docker run -dit --name $APP_NAME -p 8081:80 $APP_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
