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
    }
}
