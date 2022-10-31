pipeline {
    agent any
    stages {
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t image-builder --target builder .'
            }
        }
        stage('Test stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t image-testing --target test .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t inewthinker/todo-fe:jenkins-$BUILD_NUMBER --target delivery .'
            }
        }
        stage('Cleanup') {
            steps {
                sh 'docker system prune -f'
            }
        }
        stage('push') {
            environment {
                dockerpwd = credentials('docker_hub_crd')
            }
            steps {
                    sh 'docker login -u inewthinker -p ${dockerpwd}'
                    sh "docker push inewthinker/todo-fe:jenkins-$BUILD_NUMBER"
        }
    }
}
}
