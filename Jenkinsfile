pipeline {
    agent any

    options {
        timeout(time: 30, unit: 'MINUTES')
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
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cread01',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        cd blog
                        docker build -t kb-image04 .
                        docker tag kb-image04 kbsingh10/kb-image04:v1
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push kbsingh10/kb-image04:v1
                        docker logout
                    '''
                }
            }
        }
	stage ('copy deploy.yaml to kubernetes') {
	     steps {
	     sh	'scp deploy.yaml ec2-user@10.0.1.7:/home/ec2-user/'
	     sh 'kubectl apply -f ~/deploy.yaml'
		
		}
	}


    }
}
