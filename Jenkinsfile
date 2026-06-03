pipeline {
agent any


environment {
    DOCKER_IMAGE = "ashlesh36/backend-service:latest"
}

stages {

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t $DOCKER_IMAGE app/backend'
        }
    }

    stage('Push to Docker Hub') {
        steps {
            withCredentials([usernamePassword(
                credentialsId: 'dockerhub-creds',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS'
            )]) {
                sh '''
                echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                docker push $DOCKER_IMAGE
                '''
            }
        }
    }

    stage('Deploy to kubernetes') {
        steps {
            sh '''
            kubectl apply -f deployment.yml
            kubectl apply -f service.yml
            '''
        }
    }
}


}
