pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Run Containers') {
            steps {
                // Stop any old containers first (ignore errors if none exist)
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Optional: Clean dangling images/containers if you want
            sh 'docker system prune -af || true'
        }
        success {
            echo '✅ MERN stack deployed successfully using Docker Compose!'
        }
        failure {
            echo '❌ Build failed. Check logs above.'
        }
    }
}
