pipeline {
    agent any
    docker {
    environment {
        DOCKERHUB = credentials('docker_creds')
    }
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

        stage('Build image') {
            steps {
                unstash 'source'
                sh '''
                ls -ltr build/libs/
                docker image build -t gvindio/springboot:latest .
                docker login -u $DOCKERHUB_USR -p $DOCKERHUB_PSW
                docker push gvindio/springboot:latest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sshagent(credentials: ['docker-ssh']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@52.91.131.107 uptime'
                    sh 'ssh -v ubuntu@52.91.131.107'
                    sh 'sudo docker container run -d -p 8081:8080 --name springboot1 gvindio/springboot:latest'
                }
            }
        }
    }
}
