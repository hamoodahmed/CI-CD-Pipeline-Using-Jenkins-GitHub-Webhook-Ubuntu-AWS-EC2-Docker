pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nesths-image"
        EMAIL = "hamoodahmed75a@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo'){
            steps{
                git branch: 'main',
                url: 'https://github.com/hamoodahmed/CI-CD-Pipeline-Using-Jenkins-GitHub-Webhook-Ubuntu-AWS-EC2-Docker.git' 
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }
        stage('Stop & Remove Previous Container') {
            steps {
                bat '''
                    docker stop %CONTAINER_NAME% || exit 0
                    docker rm %CONTAINER_NAME% || exit 0
                 '''
            }
        }
        stage('Docker Container Run') {
            steps {
                bat '''
                    docker run -d -p %PORT%:%PORT%
                    --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }
         stage('Send Email Notification') {
            steps {
                emailext(
                    subject: "NestJS App Deployed Successfully on EC2!",
                    body: "Your Nest JS app is Deployed! http://localhost:${PORT}/",
                    to: "${EMAIL}"
                )
            }
        }
    }
}
