pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = "yourdockerhubusername/jenkins-sample-app" // replace with your DockerHub username
    }
    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                echo "Logging into DockerHub..."
                sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                echo "Pushing Docker image..."
                sh 'docker push $IMAGE_NAME:$BUILD_NUMBER'
            }
        }
        stage('Deploy Container') {
            steps {
                echo "Deploying Docker container locally..."
                sh 'docker rm -f sampleapp || true' // remove existing container if exists
                sh 'docker run -d -p 5000:5000 --name sampleapp $IMAGE_NAME:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            echo "Pipeline finished."
        }
    }
}
