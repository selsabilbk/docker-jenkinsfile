pipeline {

     agent {
        dockerfile {
            filename 'Dockerfile.jenkinsAgent'
            additionalBuildArgs  '--build-arg JENKINSUID=`id -u jenkins` --build-arg JENKINSGID=`id -g jenkins` --build-arg DOCKERGID=`stat -c %g /var/run/docker.sock`'
            args '-v /var/run/docker.sock:/var/run/docker.sock -u jenkins:docker'
        }
}
   

     
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }
     stage('Initialize'){
        def dockerHome = tool 'mydocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

      def  app = docker.build("nexus-docker.minikube/hellonode")
    }

   

       stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('http://nexus.minikube/', 'admin') {
            app.push("${shortCommit}")
            app.push("latest")
        }
    }

}
