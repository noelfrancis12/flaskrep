
pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "noelzzz/flask-web-app:${BUILD_NUMBER}"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/noelfrancis12/flaskrep.git', branch: 'main'
            }
        }
        stage('Verify Files') {
            steps {
                sh 'ls -la'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-password', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh """
                    echo "$DOCKER_PASSWORD" | docker login -u $DOCKER_USERNAME --password-stdin
                    docker push ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
