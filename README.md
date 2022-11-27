# todos app
Devops Seminar Final project
Steps:
•	run the Docker-pipeline via Jenkins to make sure all stages are working properly.
•	the push stage is absent from Jenkinsfile so has to be done manually or add the following:

•	stage('PUSH STAGE') {
•	 steps {
•	     sh '''
•	        docker tag [image] [yourRepo/todo-fe]:jenkins-${BUILD_NUMBER}
•	        docker login -u ${username} -p ${password}
•	        docker push [yourRepo/todo-fe] --all-tags
•	       '''
•	}
or
 environment{
 
 	registry = "<dockerhub-username>/<repo-name>"
 	registryCredential = '<dockerhub-credential-name>'        
 	}
 stage('PUSH STAGE') {
   steps{
     script {
 	   docker.withRegistry( '', registryCredential ) {
  	   dockerImage.push()
   	}
 }
•	if all went well, go to the second part of the project and do the same thing:

(the Dockerfile spec is inside the backend folder) https://github.com/inewthinker/todo-be
now the last step is to make sure is all parts can now run our Todo-app.

•	use the docker-compose.yaml file
•	  docker-compose pull
•	  docker-compose up -d

note: inside docker-compose.yaml make the according changes if you wish to use your images or other properties.
and finally browse locally: http://localhost:3000/
or remote env: http://REMOTEIP:3000/

