pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/M-Abdullah03/simple-reactjs-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat 'docker build -t %DOCKER_USERNAME%/my-react-app .'
                }
            }
        }
        stage('Run Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat 'docker run -d %DOCKER_USERNAME%/my-react-app'
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                    bat 'docker push %DOCKER_USERNAME%/my-react-app'
                }
            }
        }
    }
}