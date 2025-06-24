pipeline {
    agent any

    environment {
        KUBECONFIG = "${env.WORKSPACE}/.kubeconfig"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ovodom/brightweb-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("brightweb:latest")
                }
            }
        }

        stage('Apply Kubernetes Config') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    sh 'kubectl apply -f k8s/deployment.yaml'
                }
            }
        }
    }
}
