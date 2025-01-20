pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/your-repo-url.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def appName = "my-app"
                    def dockerImage = docker.build("${appName}:latest")
                }
            }
        }
        stage('Test Docker Image') {
            steps {
                script {
                    sh 'docker run --rm my-app:latest'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker tag my-app:latest your-dockerhub-repo/my-app:latest'
                    sh 'docker push your-dockerhub-repo/my-app:latest'
                }
            }
        }
    }
}
