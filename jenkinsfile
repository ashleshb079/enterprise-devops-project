pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t backend-service app/backend'
            }
        }
    }
}