pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SanthiS123/jenkins-sample-app.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
}
