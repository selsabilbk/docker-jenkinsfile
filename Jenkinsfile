
pipeline {
    agent any
    stages {
          stage('Clone repository') {
              steps {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }}
        stage('Acitivate socket')
        {
              steps {
    sh 'chmod 777 /var/run/docker.sock'
}}
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
