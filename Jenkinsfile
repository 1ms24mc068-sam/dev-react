pipeline {
    agent any
    environment {
        DOCKERHUB_CRED = credentials('dockerhub')
        IMAGE_NAME = "sam1199/dev-react"
    }

    // triggers {
    //     cron ('* * * * *')
    // }
    
    stages {
        stage('checkout') {
            steps { git url: 'https://github.com/1ms24mc068-sam/dev-react', branch: 'main' }
        }
        stage('Build Docker Image') {
            steps {
                script { dockerImage = docker.build("${IMAGE_NAME}:latest") }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
    post {
        success { echo "Pipeline Successful" }
        failure { echo "Pipeline Failed" }
        always { deleteDir() }
    }
}
