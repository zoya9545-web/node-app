pipeline {
    agent any

    environment {
        IMAGE_NAME = "zoya9545/node-app:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/zoya9545-web/node-app.git',
                    branch: 'main',
                    credentialsId: 'github-creds'
                )
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'docker-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "Stopping old container if exists..."
                    docker stop node-app || true
                    docker rm node-app || true

                    echo "Pulling latest image..."
                    docker pull zoya9545/node-app:latest

                    echo "Starting new container..."
                    docker run -d -p 3000:3000 --name node-app zoya9545/node-app:latest
                '''
            }
        }
    }
}
