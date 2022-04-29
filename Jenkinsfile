node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("eliyagervas/azure-app-jenkins")
    }

    /*stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }
    */

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
