pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "satyamgupta9012@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo') {
            steps{
                git branch: 'main' , url: 'https://github.com/Neofighter1/CI_CD_Pipeline_Using_Jenkins_Docker_GitHub_Webhook_Ubuntu_AWS_EC2.git'
            }
        }

        stage('Build Docker Image') {
            steps{
                sh 'docker build -t $IMAGE_NAME'
            }
        }
        stage('Stop & Remove Previous Container') {
            steps{
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }
        stage('Docker Container Run') {
            steps{
                sh '''
                    docker run -d -p ${PORT}:${PORT}
                    --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        stage('Send Email Notification') {
            steps{
                emailtext(
                    subject: "NestJS APP Deployed Successfully!"
                    body: "Your Nest JS app is Deployed! 
                    http://3.82.150.57:${PORT}/"
                    to: "${EMAIL}"
                )
            }
        }
        
    }
}