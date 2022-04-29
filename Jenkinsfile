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
    stage('Run trivy') {
        steps{

        sh(script:"""
              trivy eliyagervas/azure-app-jenkins
              """
             )
        }
    }
    stage('Push image') {
        /* You would need to first register with DockerHub before you can push images to your account */
        docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub-ID') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
