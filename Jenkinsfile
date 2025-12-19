pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LohadeDarshan/Deploying-a-Python-Web-Application.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myserverd/python-app .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry(url: 'https://index.docker.io/v1/', credentialsId: 'dockerHubCred') {
                    sh 'docker tag myserverd/python-app:latest myserverd/python-app:latest'
                    sh 'docker push myserverd/python-app:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f k8s/deployment.yaml
                    kubectl apply -f k8s/service.yaml
                '''
            }
        }
    }
}
