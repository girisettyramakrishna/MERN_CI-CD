pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')  // Jenkins stored credentials
        IMAGE_NAME_BACKEND = "yourdockerhubuser/mern-backend"
        IMAGE_NAME_FRONTEND = "yourdockerhubuser/mern-frontend"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@https://github.com/girisettyramakrishna/MERN_CI-CD.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME_BACKEND ./backend'
                    sh 'docker build -t $IMAGE_NAME_FRONTEND ./react_redux'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push $IMAGE_NAME_BACKEND'
                    sh 'docker push $IMAGE_NAME_FRONTEND'
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }
}
