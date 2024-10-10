pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')  // Reference DockerHub credentials
    }
    stages {
        stage('Clone from GitHub') {
            steps {
                git 'https://github.com/akor92/akor92.git'  // Replace with your GitHub repo URL
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image without specifying a tag
                    def image = docker.build("akor92/portfolio")
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    // Use the DockerHub credentials to push the image
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKERHUB_CREDENTIALS') {
                        image.push()  // Push the image (default tag is 'latest')
                    }
                }
            }
        }
    }
}
