pipeline {
    agent any

    environment {
        DOCKERHUB = credentials('docker_creds')
    }

    options {
        timestamps()
        skipDefaultCheckout(true)
    }

    stages {
        stage('Build code') {
            agent {
                docker {
                    image 'gradle:jdk15'
                }
            }
        }
    }
}
           
