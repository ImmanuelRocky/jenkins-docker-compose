pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "rockyimman/test-flask-app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ImmanuelRocky/jenkins-docker-compose.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push rockyimman/test-flask-app'
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
