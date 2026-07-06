pipeline {

    agent any

    environment {
        IMAGE_NAME = "python-flask-app"
        CONTAINER_NAME = "python-container"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mohanbarani/jenkinspip.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker run -d \
                --name $CONTAINER_NAME \
                -p 5000:5000 \
                $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful'
        }

        failure {
            echo 'Deployment Failed'
        }
    }
}
