
pipeline {
    agent any
    stages {
          stage('Clone repository') {
              steps {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }}
     stage('Initialize'){
         steps {
             script {
        def dockerHome = tool 'mydocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }} }

        stage('Build image') {
            steps {
                echo 'Starting to build docker image'

                script {
                    def customImage = docker.build("my-image:${env.BUILD_ID}")
                    customImage.push()
                }
            }
        }
    }
}
