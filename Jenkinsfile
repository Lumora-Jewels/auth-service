pipeline {
    agent any

    environment {
        SERVICE_NAME = 'auth-service'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "https://github.com/Lumora-Jewels/${SERVICE_NAME}.git"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'yarn install'
            }
        }

        stage('Build') {
            steps {
                sh 'yarn build || echo "No build script, continue"'
            }
        }

        stage('Deploy') {
            steps {
                sh """
                pm2 stop ${SERVICE_NAME} || true
                pm2 start yarn --name ${SERVICE_NAME} -- start
                pm2 save
                """
            }
        }
    }
}
