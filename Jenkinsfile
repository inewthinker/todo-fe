pipeline {
    agent any

    stages {
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t inewthinker/todo-fe:latest --target builder .'
            }
        }
        stage('Test stage') {
            steps {
                 sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t inewthinker/todo-fe:latest --target test .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline -t inewthinker/todo-fe:latest --target delivery .'
            }
        }
        stage('run') {
            steps {
                sh docker run -d inewthinker/todo-fe
                
            }
        }
        stage('push-image-to-repo') {
            steps {
                sh (script:"set +x && docker login -u ${username} -p ${pass} && set -x")
                sh docker tag inewthinker/todo-fe inewthinker/todo-fe:jenkins-${BUILD_NUMBER}
                    
                   docker push inewthinker/todo-fe --all-tags
            }
        }
          stage('Cleanup stage') {
            steps {
                sh 'yes | docker system prune '
            }
        }
    }
}
