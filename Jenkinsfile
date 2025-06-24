pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ovodom/brightweb-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("brightweb:latest")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker rm -f brightweb || true'
                    sh 'docker run -d --name brightweb -p 80:80 brightweb:latest'
                }
            }
        }
    }
}
