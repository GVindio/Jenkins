pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from a Git repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Build the code (echo a message in this example)
                sh 'echo "Building the code..."'
            }
        }

        stage('Test') {
            steps {
                // Run a test (echo a message in this example)
                sh 'echo "Running tests..."'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive build artifacts (e.g., test reports, binaries)
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            // Display a success message
            echo 'Pipeline succeeded! Tests passed.'
        }
        failure {
            // Display a failure message
            echo 'Pipeline failed! Tests may have failed.'
        }
    }
}

