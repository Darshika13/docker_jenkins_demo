pipeline {
     agent any
     environment {
         GIT_REPOSITORY_URL = 
'https://github.com/Darshika13/docker_jenkins_demo.git'
        DOCKER_IMAGE_NAME = 'Darshika13/docker_jenkins_demo'
        IMAGE_TAG = '1.0'
    }
    stage {
        stage('Clone Repository') {
            steps {
                script {
                    try {
                         git branch: 'main', url:GIT_REPOSITORY_URL
                    } catch (Exception e) {
                        echo "Failed to clone repository: ${e.message}"
                        error "Failed to clone repository"
                     }
                   }
             }
       }
       stage('Push to DockerHub') {
           steps {
                script {
                     try {
                          withCredentials([usernamePassword(credentialsId: 'my-docker-hub-credentials-id', usernameVariable: 'DOCKER_USERNAME',passwordVariable: 'DOCKER_PASSWORD' )]) {
                                                           //explicit login before push
                                                            sh """
                                                            echo "$DOCKER_PASSWORD" | docker login -u
"$DOCKER_USERNAME" --password-stdin
                            docker push ${DOCKER_IMAGE_NAME}:${IMAGE_TAG}
                            """
                     }
                 } catch (Exception e) {
                     echo "Failed to push Docker image to registry"
${e.message}"
                     error "Failed to push Docker image"
                 } } } } } }
