pipeline {
    agent any

    environment {
        APP_NAME = "myapp"
        IMAGE_TAG = "v${BUILD_NUMBER}"
    }

    stages {

        stage("Clone Code") {
            steps {
                git 'https://github.com/raufmalik002/Dev-Project.git'
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

                docker stop $APP_NAME || true
                docker rm $APP_NAME || true

                docker run -d -p 5000:5000 --name $APP_NAME $APP_NAME:$IMAGE_TAG
                '''
            }
        }
    }
}