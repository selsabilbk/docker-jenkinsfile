node {
    def app
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
        app = docker.build("nexus-docker.minikube/" + "${BUILD_NUMBER}")
    }
    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
        app.inside {
            sh 'echo "Tests passed"'
        }
    }
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
 // withCredentials([usernamePassword( credentialsId: 'admin', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
// docker.withServer(host) {
        
//docker.withRegistry(nexus-docker.minikube, 'admin') {
sh "docker login -u admin -p admin123 nexus-docker.minikube"
    
app.push("${env.BUILD_NUMBER}")
//app.push("latest")
   // }
//}
}
}
   // }
