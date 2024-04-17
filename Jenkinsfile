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
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("my-react-app")
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    docker.image("my-react-app").run()
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("my-react-app").push()
                    }
                }
            }
        }
    }
}