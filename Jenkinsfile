pipeline {
    agent any
    environment {
        DOCKER_HOST = 'unix:///var/run/docker.sock'
        DOCKER_REGISTRY = 'https://index.docker.io/v1/'
        DOCKER_CREDENTIALS_ID = 'Docker-sec' 
    }
    tools {
        dockerTool 'docker'
    }
    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    dir('src') {

                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t aannuu/cartservice:latest ."
                    }
                        }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push aannuu/cartservice:latest "
                    }
                }
            }
        }
    }
}
