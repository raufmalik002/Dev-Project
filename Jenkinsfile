pipeline {
    agent any

    environment {
        APP_NAME = "myapp"
        IMAGE_TAG = "v${BUILD_NUMBER}"
    }

    stages {

        stage("Clone Code") {
            steps {
                git branch: 'main', url: 'https://github.com/raufmalik002/Dev-Project.git'
            }
        }

        stage("Build") {
            steps {
                sh '''
                echo "Building version: $IMAGE_TAG"
                docker build -t $APP_NAME:$IMAGE_TAG .
                docker tag $APP_NAME:$IMAGE_TAG $APP_NAME:latest
                '''
            }
        }

        stage("Deploy") {
            steps {
                sh '''
                echo "Deploying version: $IMAGE_TAG"

                docker-compose down || true
                docker-compose up -d
                '''
            }
        }
    }
}