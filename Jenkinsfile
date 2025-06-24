pipeline {
    agent {
        docker {
            image 'bitnami/kubectl:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
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
                    def dockerImage = docker.build("brightweb:latest")
                }
            }
        }

        stage('Apply Kubernetes Config') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
