pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/vishalforaws333-debug/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app:latest .'
            }
        }

        stage('Push to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region ap-south-1 | \
                docker login --username AWS --password-stdin 424135051837.dkr.ecr.ap-south-1.amazonaws.com

                docker tag flask-app:latest 424135051837.dkr.ecr.ap-south-1.amazonaws.com/flask-app:latest
                docker push 424135051837.dkr.ecr.ap-south-1.amazonaws.com/flask-app:latest
                '''
            }
        }
    }
}

