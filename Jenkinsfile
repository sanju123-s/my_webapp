pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = '3ae068b0-d90d-43fd-83c0-ec128e92474f'
        IMAGE_NAME = 'sanju413/my_webapp'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sanju123-s/my_webapp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                    docker --version
                    docker build -t ${IMAGE_NAME}:latest .
                """
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: DOCKERHUB_CREDENTIALS,
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
