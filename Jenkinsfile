pipeline {
	agent any
	environment {
		GIT_REPOSITORY_URL =
'https://github.com/Darshika13/docker_jenkins_demo.git'
	DOCKER_IMAGE_NAME = 'Darshika13/docker_jenkins_demo'
	IMAGE_TAG = '1.0'
    }
    stages {
	stage('Clone Repository') {
	    steps {
		script {
		    try {
			git branch: "main", url:https://github.com/Darshika13/docker_jenkins_demo.git
		    } catch (Exception e) {
			echo "Fail to clone repository: ${e.message}"
			error "Fail to clone repository"
		    }
		}
	   }
    }
    stage('Build Docker Image') {
	steps {
	    script {
		try {
		    docker.build("${DOCKER_IMAGE_NAME}: ${IMAGE_TAG}")
		} catch (Exception e) {
		    echo "Falied to build docker image: ${e.message}"
		    error "Failed to build docker image"
}
}
}
}
stage('Push to DockerHub') {
steps {
script {
try {
withCredentials([usernamePassword(credentialsId: 'my-docker-hub-credebtials-id', usernameVariable: 'Darshika13', passVariable: 'Janu@1910')]) {
sh """
echo "DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
docker push (Darshika13/docker_jenkins_demo):{1.0}
"""
}
} catch ( Exception e ) {
echo " Failed to push docker image to registry:"$(e.message)
error "failed to push docker image"
}
}
}
}



