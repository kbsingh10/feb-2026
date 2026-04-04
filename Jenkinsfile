pipeline {
    agent any
	stages {
           stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kbsingh10/feb-2026.git',
                    credentialsId: ‘git-cred01'
            }
        }
        stage('Check Files') {
        steps {
        sh 'ls -ltr'
        sh 'docker ps'
        }
        }
  }
}
