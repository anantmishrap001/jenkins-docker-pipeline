pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'python3 app/main.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'pytest app/test_app.py'
            }
        }

        stage('Dockerize') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t demo-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application (simulated)...'
                sh 'echo "App deployed successfully!"'
            }
        }
    }
}
