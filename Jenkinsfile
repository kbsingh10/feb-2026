pipeline {
    agent any

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

	stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-01',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
		    sudo docker build -t kb-image .
                    sudo docker image tag kb-image kbsingh10/kb-image:v1
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    sudo docker push kbsingh10/kb-image:v1
                    sudo docker logout
                    '''
                }
            }
        }

    }
}
