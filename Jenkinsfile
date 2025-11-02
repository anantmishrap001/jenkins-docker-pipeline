pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
                sh '''
                    pip install --upgrade pip
                    pip install -r requirements.txt
                    python3 app/main.py
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '''
                    pytest app/test_app.py
                '''
            }
        }

        stage('Dockerize') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t jenkins-pipeline-demo .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'docker run -d -p 5000:5000 jenkins-pipeline-demo'
            }
        }
    }
}
