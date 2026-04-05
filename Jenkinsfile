pipeline {
    agent any

    options {
        timeout(time: 30, unit: 'MINUTES')
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kbsingh10/feb-2026.git',
                    credentialsId: 'git-cred01'
            }
        }

        stage('Check Files') {
            steps {
                sh 'ls -ltr'
                sh 'docker ps'
            }
        }

        stage('Docker Build & Push') {
            options {
                timeout(time: 20, unit: 'MINUTES')
            }
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-01',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        cd blog
                        docker build -t kb-image01 .
                        docker image tag kb-image01 kbsingh10/kb-image01:v1
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push kbsingh10/kb-image01:v1
                        docker logout
                    '''
                }
            }
        }

    }
