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
                // Add your build steps here
                // For example, you can build your code with Gradle:
                // sh 'gradle clean build'
            }
        }
    }
}
