pipeline {
    agent any

    environment {
        IMAGE_NAME = "todo-django-app"
        CONTAINER_NAME = "todo_app"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:nehanayak07/todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                }
            }
        }

        stage('Run Docker') {
            steps {
                script {
                    sh "docker run -d -p 8081:8000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:latest"
                }
            }
        }
    }

    post {
        success {
            echo "🎉 Deployment succeeded."
        }
        failure {
            echo "❌ Deployment failed."
        }
    }
}
