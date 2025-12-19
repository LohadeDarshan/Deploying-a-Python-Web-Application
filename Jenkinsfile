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
        stage('Run Container') {
            steps {
                sh '''
                    docker stop python-app-container || true
                    docker rm python-app-container || true
                    docker run -d --name python-app-container -p 5000:5000 adeeti-jwellers
                '''
            }
        }
    }
}
