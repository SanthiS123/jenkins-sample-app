pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = "santhi311/jenkins-sample-app" // replace with your DockerHub username
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SanthiS123/jenkins-sample-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
            }
        }
        stage('Push') {
            steps {
                sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                sh 'docker push $IMAGE_NAME:$BUILD_NUMBER'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 --name sampleapp $IMAGE_NAME:$BUILD_NUMBER'
            }
        }
    }
}
