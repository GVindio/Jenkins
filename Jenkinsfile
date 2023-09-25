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

            steps {
                cleanWs()
                checkout scm
                sh 'chmod +x gradlew'
                sh './gradlew build'
                sh 'ls -ltr build/libs/'
                stash 'source'
            }
        }
    }
}
