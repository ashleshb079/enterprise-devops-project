pipeline {
agent any


stages {
    stage('Build Docker Image') {
        steps {
            sh 'docker build -t backend-service app/backend'
        }
    }

    stage('Run Container') {
        steps {
            sh '''
            docker rm -f backend-container || true
            docker run -d --name backend-container -p 3000:3000 backend-service
            '''
        }
    }
}

}
