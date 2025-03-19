pipeline {
    agent any

    environment {
        IMAGE_NAME = "harinim2405/my-app"
        REGISTRY = "docker.io"
        APP_DIR = "/home/vboxuser/Documents/jenkins"
        DOCKER_USER = "harinim2405"          // Replace with your Docker Hub username
        DOCKER_PASS = "Harini@2405"          // Replace with your Docker Hub password
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/HARINIM2405/JENKINS', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME:latest ."
                }
            }
        }

        stage('Login to Docker Registry') {
            steps {
                script {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to Docker Registry') {
            steps {
                script {
                    sh "docker push $IMAGE_NAME:latest"
                }
            }
        }

        stage('Deploy using Docker Compose') {
            steps {
                script {
                    sh "docker-compose up -d"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check the logs for errors.'
        }
    }
}
