pipeline {
    agent any
    environment {
        IMG_NAME = 'my-lab-image'
        DOCKER_REPO = 'devops317/labs-images'
    }
    stages {
        stage('build') {
            steps {
                script {
                        sh 'docker build -t ${IMG_NAME} .'
                        sh 'docker tag ${IMG_NAME} ${DOCKER_REPO}:${IMG_NAME}'
                }
            }
        }
        stage('push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'PSWD', usernameVariable: 'LOGIN')]) {
                    script {
                        sh 'echo ${PSWD} | docker login -u ${LOGIN} --password-stdin'
                        sh 'docker push ${DOCKER_REPO}:${IMG_NAME}'
                    }
                }
            }
        }
    }
}
