pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        IMAGE_NAME = "todo-django-app"
        CONTAINER_NAME = "todo_app"
        APP_PORT = "8081"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/nehanayak07/todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop Old Container') {
            steps {
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }

        stage('Deploy New Container') {
            steps {
                sh "docker run -d -p ${APP_PORT}:8000 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo "✅ Auto CI/CD Deployment successful"
        }
        failure {
            echo "❌ Auto CI/CD Deployment failed"
        }
    }
}

