node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }
   
   

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("resuanusha/webpage")
    }

    

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        
        
   stage('RunningImages ') {
       sh '''
         docker pull resuanusha/webpage:latest
         docker run -d -p 2222:80 resuanusha/webpage
       
       '''
         }      
    }
}
