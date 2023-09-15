
pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                echo 'building the application'
                sh'docker build -t myimage .'
            }
        }
        stage('deploy') {
            steps {
                echo 'deploying the application'
                sh'docker-compose up -d '
            }
        }
        stage('push') {
            steps {
                withCredentials([usernamePassword(credentialsId: "dockerhub", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                 sh "echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin docker.io"
                  sh 'docker push myimage'
                }   
            }
        }

    }
    post {
        always{
            sh 'docker logout'
        }
    }
}