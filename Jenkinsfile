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

        stage('Docker tag image') {
            steps {
                script {
                    sh 'docker tag uadb:v1 momozizou/uadb:v1'
                    sh 'docker images'
                }
            }
        }

         stage('Docker push image') {
            steps {
                script {
                    sh 'docker push momozizou/uadb:v1'
                }
            }
        }

        stage('Déploiement de l\'application') {
            steps {
                script {
                    sh 'kubectl apply -f ./manifests/deployment.yml'
                }
            }
        }

         stage('Déploiement du service') {
            steps {
                script {
                    sh 'kubectl apply -f ./manifests/service.yml'
                }
            }
        }

    }
}