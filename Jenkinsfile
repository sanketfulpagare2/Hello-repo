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

        stage('Push Image to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerKey', variable: 'dockerKey')]) {
                    sh '''
                      docker login -u sanketfulpagare2 -p ${dockerKey}
                      docker tag helloapp sanketfulpagare2/helloapp:latest
                      docker push sanketfulpagare2/helloapp:latest
                      docker logout
                    '''
                }
            }
        }

        stage('Deploy Docker on EC2') {
            agent { label 'ec2' }

            steps {
                sh '''
                  docker pull sanketfulpagare2/helloapp:latest || true
                  docker rm -f helloapp || true
                  docker run -d \
                    --name helloapp \
                    -p 8000:8000 \
                    sanketfulpagare2/helloapp:latest
                '''
            }
        }

    }
}
