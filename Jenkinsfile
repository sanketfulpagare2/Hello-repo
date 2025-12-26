 pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t helloapp .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f helloapp || true
                docker run -d -p 8000:8000 --name helloapp helloapp
                '''
            }
        }
    }
}
