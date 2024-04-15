pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sheraztariq22/simple-reactjs-app-jenkins.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("my-react-app:latest")
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'npm start'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'my-docker-hub-credentials') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
