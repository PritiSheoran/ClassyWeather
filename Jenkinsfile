pipeline {
    agent any

    environment {
        DOCKER_IMAGE = '23mcc20042/weather'  
        DOCKER_CREDENTIALS_ID = 'Weather'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from version control
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the repository
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('', DOCKER_CREDENTIALS_ID) {
                        echo 'Logged in to Docker Hub'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the image to Docker Hub
                    docker.withRegistry('', DOCKER_CREDENTIALS_ID) {
                        def customImage = docker.image(DOCKER_IMAGE)
                        customImage.push("latest")  // Push the image with the 'latest' tag
                    }
                }
            }
        }
    }
}
