pipeline {
    agent any

    stages {
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Docker-pipeline -t inewthinker/todo-fe:latest --target builder .'
            }
        }
        stage('Test stage') {
            steps {
                 sh 'DOCKER_BUILDKIT=1 docker build -f Docker-pipeline -t inewthinker/todo-fe:latest --target test .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f Docker-pipeline -t inewthinker/todo-fe:latest --target delivery .'
            }
        }
          stage('Cleanup stage') {
            steps {
                sh 'yes | docker system prune '
            }
        }
    }
}
