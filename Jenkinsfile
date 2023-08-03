pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'hub.docker.com/r/tusharnayak1515/maadhar-client'
        DOCKER_IMAGE_TAG = 'latest'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    bat 'npm install'
                    bat 'npm run build --prod'
                }
            }
        }

        stage('Dockerize') {
            steps {
                script {
                    def dockerImage
                    dockerImage = docker.build("${DOCKER_REGISTRY}:${DOCKER_IMAGE_TAG}")

                    docker.withRegistry("${DOCKER_REGISTRY}", "6c5bb7c1-b4ff-4885-accf-f0516ad093bd") {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
