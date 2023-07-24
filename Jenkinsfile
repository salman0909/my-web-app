pipeline {
    agent any

    environment {
        dockerhubCredentials = 'dockerhub-credentials'
        dockerImageTag = "salman1091/my-web-app:${env.BUILD_TAG.toLowerCase()}"
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Make sure to replace 'your-repo-url' with the URL of your Git repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/salman0909/my-web-app.git']]])
                }
            }
        }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $dockerImageTag ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', dockerhubCredentials) {
                        sh "docker push $dockerImageTag"
                    }
                }
            }
        }
    }
}



