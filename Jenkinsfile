pipeline {
    agent any

    triggers {
            pollSCM('* * * * *')
        }
    stages {
        stage('Collect') {
            steps {
                sh "mkdir -p log"
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
                sh 'docker run --name="pysnake" pysnake'
                sh 'docker logs pysnake > ./log/pysnake_log.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'cd ./test'
                sh 'docker build -t pysnake-test .'
                sh 'docker run --name="pysnake-test" pysnake-test'
                sh 'docker logs pysnake-test > ./log/pysnake_deploy_log.txt'
            }
        }
        stage('Deploy'){
            steps {
                sh 'cd ./deploy'
                sh 'docker build -t pysnake-deploy .'
                sh 'docker run --name="pysnake-deploy" pysnake-deploy'
                sh 'docker logs pysnake-deploy > ./log/pysnake_test_log.txt'
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
