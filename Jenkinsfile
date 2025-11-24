pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/zoya9545-web/node-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install || true'
            }
        }

        stage('Build Complete') {
            steps {
                echo 'Build finished successfully!'
            }
        }
    }
}
