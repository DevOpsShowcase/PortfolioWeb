
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'github-website'
        CONTAINER_NAME = 'github-website-container'
        APP_PORT = '8080'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code downloaded from GitHub.'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    sudo docker build \
                      -t ${IMAGE_NAME}:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Remove Old Container') {
            steps {
                sh '''
                    sudo docker rm -f ${CONTAINER_NAME} || true
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    sudo docker run -d \
                      --name ${CONTAINER_NAME} \
                      --restart unless-stopped \
                      -p ${APP_PORT}:80 \
                      ${IMAGE_NAME}:${BUILD_NUMBER}
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    sudo docker ps
                    sudo docker logs --tail 20 ${CONTAINER_NAME}
                '''
                echo 'Deployment pipeline completed.'
            }
        }
    }
}
