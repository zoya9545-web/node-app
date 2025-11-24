pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/zoya9545-web/node-app.git',
                    credentialsId: '6404498d-ac8d-4f2e-be03-4e9a3fcd2c65'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Complete') {
            steps {
                echo 'Build finished successfully!'
            }
        }
    }
}
