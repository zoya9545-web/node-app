pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "zoya9545/node-app"
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

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub',
