pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-jenkins-app"
        CONTAINER_NAME = "flask_jenkins_container"
        PORT = "5000"
    }

    stages {

        stage('Checkout') {
            steps {
                echo '📦 Cloning repository...'
                git branch: 'main', url: 'https://github.com/anantmishrap001/jenkins-docker-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🐳 Building Docker image...'
                sh 'docker build -t ${IMAGE_NAME} .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo '🧹 Removing old container if exists...'
                sh '''
                if [ "$(docker ps -aq -f name=${CONTAINER_NAME})" ]; then
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                fi
                '''
            }
        }

        stage('Run Container') {
            steps {
                echo '🚀 Running new Flask container...'
                sh 'docker run -d --name ${CONTAINER_NAME} -p ${PORT}:5000 ${IMAGE_NAME}'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo '🔍 Checking running containers...'
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Visit: http://localhost:${PORT}"
        }
        failure {
            echo "❌ Deployment failed. Check logs above."
        }
    }
}
