pipeline {
    agent any

    triggers {
            pollSCM('* * * * *')
        }
    stages {
        stage('Collect') {
            steps {
                sh "docker container prune -f"
                sh "docker image prune -af"
            }
        }
        
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
