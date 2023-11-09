pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the application..."'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t sample-web-app .'
                sh 'docker tag sample-web-app $DOCKER_TAG'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockerhub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker push bhavani4444/sample-web-app'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 80:80 bhavani4444/sample-web-app'
            }
        }
    }
}
