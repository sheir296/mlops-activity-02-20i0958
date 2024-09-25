pipeline {
    agent any

    environment {
        DOCKER_USERNAME = credentials('docker-username')
        DOCKER_PASSWORD = credentials('docker-password')
    }

    stages {
        stage('Checkout repository') {
            steps {
                checkout scm
            }
        }

        stage('Set up Docker Buildx') {
            steps {
                sh '''
                docker buildx create --use
                '''
            }
        }

        stage('Log in to Docker Hub') {
            steps {
                sh '''
                echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                '''
            }
        }

        stage('Build and push Docker image') {
            steps {
                sh '''
                docker buildx build --push --tag $DOCKER_USERNAME/basic-ml-app:latest .
                '''
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
