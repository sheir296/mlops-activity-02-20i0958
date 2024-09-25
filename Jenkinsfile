pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sheir296/mlops-activity-02-20i0958.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                        docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                        docker build -t $DOCKER_USERNAME/my-image .
                        docker push $DOCKER_USERNAME/my-image
                        """
                    }
                }
            }
        }
    }
}
