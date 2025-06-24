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
                sh 'docker build -t brightweb:latest .'
            }
        }

        stage('Apply Kubernetes Config') {
            agent {
                docker {
                    image 'bitnami/kubectl:latest'
                    args '--entrypoint=""'
                }
            }
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
