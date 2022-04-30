node {
    def app
	

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */
	 echo "Start Cloning repository"   

        checkout scm
	    
	 echo "Finish Cloning repository"   
    }

    stage('Build image') {
	    echo "Trying to Build Docker Image"
        /* This builds the actual image */
        app = docker.build("eliyagervas/azure-app-jenkins")
	    echo "Finish Build Docker Image"
    }
		   
    stage('Push image') {
	      echo "Trying Push Docker Build to DockerHub"
        /* You would need to first register with DockerHub before you can push images to your account */
        docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub-ID') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Finish Push Docker Build to DockerHub"
    }
    
     stage('Deployment') {
	      echo "Trying to Deploy"
          acsDeploy(azureCredentialsId: "jenkins_demo", 
		    configFilePaths: "**/*.yaml", 
		    containerService: "jenkinsaks | AKS", 
		    dcosDockerCredentialsPath: "", 
		    resourceGroupName: "jenkins-app", 
		    secretName: "", 
		    sshCredentialsId: ""
		    ) 
                echo "Finish Deployment"
    }	
	
}
