pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // Uruchom docker-compose
                    bat 'docker-compose up --build'
                }
            }
        }
        stage('Test') {
            steps {

            }
        }
        stage('Deploy') {
            steps {

            }
        }
    }
}