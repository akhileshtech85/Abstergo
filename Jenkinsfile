pipeline {
    agent any

    stages {
        stage('Pre-requisite') {
            steps {
                script {
                    echo 'Checking pre-requisites...'
                    // Add commands to check dependencies, tools, or configurations
                    sh 'echo "Pre-requisite check complete"'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Starting build...'
                    // Replace with actual build commands
                    
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    // Replace with actual test commands
                    
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir() // Clean up workspace after the build
        }
        success {
            echo 'Build and tests completed successfully.'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
