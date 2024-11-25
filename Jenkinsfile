pipeline {
    agent any

    environment {
        GIT_REPOSITORY_URL = 'https://github.com/Darshika13/docker_jenkins_demo.git'
        DOCKER_IMAGE_NAME = 'Darshika13/docker_jenkins_demo'
        IMAGE_TAG = '1.0'
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    try {
                        // Cloning the Git repository
                        git branch: 'main', url: GIT_REPOSITORY_URL
                    } catch (Exception e) {
                        // Handling any errors if the git clone fails
                        echo "Failed to clone repository: ${e.message}"
                        error "Failed to clone repository"
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    try {
                        // Build the Docker image
                        sh "docker build -t ${DOCKER_IMAGE_NAME}:${IMAGE_TAG} ."
                    } catch (Exception e) {
                        echo "Failed to build Docker image: ${e.message}"
                        error "Docker build failed"
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    try {
                        // Securely handle Docker credentials with withCredentials
                        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                            // Using docker login with secure environment variables
                            sh """
                                echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin
                            """
                        }
                        // Push the Docker image to Docker Hub or a registry
                        sh "docker push ${DOCKER_IMAGE_NAME}:${IMAGE_TAG}"
                    } catch (Exception e) {
                        echo "Failed to push Docker image: ${e.message}"
                        error "Docker push failed"
                    }
                }
            }
        }
    }
}
