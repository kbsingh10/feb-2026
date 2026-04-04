pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kbsingh10/proj-feb.git',
                    credentialsId: 'git-cred01'
            }
        }
        stage('Check Files') {
        steps {
        sh 'ls -ltr'
        sh 'sudo docker ps'
        }
        }

    }
}
