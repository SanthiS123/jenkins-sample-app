pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = "your-dockerhub-username/jenkins-sample-app"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SanthiS123/jenkins-sample-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t mydockerimage:0.1 .'
            }
        }
        stage('Push') {
            steps {
                sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                sh 'docker push mydockerimage:0'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 --name sampleapp mydockerimage:0'
            }
        }
    }
}
