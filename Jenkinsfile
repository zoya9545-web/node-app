pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "node-app"
        DOCKER_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: '6404498d-ac8d-4f2e-be03-4e9a3fcd2c65',
                    url: 'https://github.com/zoya9545-web/node-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p 3000:3000 --name node-container ${DOCKER_IMAGE}:${DOCKER_TAG}"
            }
        }
    }
}
