node {
    def app
	
    environment{
       PATH = "$PATH:/var/lib/jenkins/workspace/azure_app pipeline/docker-compose.yaml"
    }

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
	    echo "Trying to Build Docker Image"
        /* This builds the actual image */
        app = docker.build("eliyagervas/azure-app-jenkins")
	    echo "Finish Build Docker Image"
    }

    stage('Run Test App') {
            echo "Trying to Test Docker Container"
	    
	        sh(script: """
		     docker-compose up
		""")
	   
	    echo "Finish Container Test"
    }
    stage('Stop Test App') {
            echo "Finish testing"
	    
	        sh(script: """
		     docker-compose down
		""")
	    
	    echo "Finish Testing"
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
}
