pipeline {
    agent any

    triggers {
            pollSCM('* * * * *')
        }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ironnext22/snakegame-gui'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t pysnake .'
            }
        }
        stage('Test') {
            steps {
                sh 'cd ./test'
                sh 'docker build -t pysnake-test .'
                sh 'docker run pysnake-test'
            }
        }
        stage('Collect') {
            steps {
            cleanWs()
            git branch: "${GIT_BRANCH}", credentialsId: "${GIT_CRED_ID}", url: "${GIT_REPO}"
            sh 'chmod +x clear.sh'
            sh './clear.sh'
            }
        }
    }

    post {
        success {
            echo 'Budowa zakończona sukcesem!.'
        }
        failure {
            echo 'Budowa nie powiodła się..'
        }
    }
}
