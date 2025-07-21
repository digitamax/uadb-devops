pipeline {
    agent {label 'docker'}

    environment {
        DOCKER_PASSWORD=credentials('DOCKER_PASSWORD')
    }

    stages {
        stage('Docker login') {
            steps {
                script {
                    sh 'echo $DOCKER_PASSWORD | docker login -u momozizou --password-stdin'
                }
            }
        }

        stage('Docker build image') {
            steps {
                script {
                    sh 'docker build -t uadb:v1 .'
                }
            }
        }
    }
}