pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nesths-image"
        EMAIL = "adnanyo5491@gmail.com"
        PORT = "3000"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/adnan54915626/CICD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '/usr/bin/docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove Previous Container') {
            steps {
                sh '''
                    /usr/bin/docker stop $CONTAINER_NAME || true
                    /usr/bin/docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Docker Container Run') {
            steps {
                sh '''
                    /usr/bin/docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Send Email Notification') {
            steps {
                emailext(
                    subject: "NestJS App Deployed Successfully on EC2!",
                    body: "Your NestJS app is deployed successfully! http://18.117.158.28:${PORT}/",
                    to: "${EMAIL}"
                )
            }
        }
    }
}g