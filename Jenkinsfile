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
                sh '''
                    pip install --upgrade pip
                    pip install -r requirements.txt
                    pytest app/test_app.py
                '''
            }
        }

        stage('Dockerize') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t jenkins-pipeline-demo .'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying Docker container...'
                sh 'docker run -d -p 5000:5000 jenkins-pipeline-demo'
            }
        }
    }
}
