pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/kbsingh10/feb-2026.git',
                    credentialsId: 'git-cred01'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'ls -ltr'
		sh 'sudo docker ps'
            }
        }
    }
}
