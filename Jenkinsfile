pipeline {
    agent any

    stages {
        stage('Job-1') {
            steps {
                script {
                    echo 'Install and configure puppet agent on slave node.'
                    // Add commands to check dependencies, tools, or configurations
                    sh 'echo "Pre-requisite check completed"'
                }
            }
        }

        stage('Job-2') {
            steps {
                script {
                    echo 'Push Ansible configuration on test-server to install docker.'
                    // Replace with actual build commands
                    
                }
            }
        }

        stage('Job-3') {
            steps {
                script {
                    echo 'Pull repo, Build docker and Deploy Container.'
                    docker build -t website .
                    docker rm -f website-test-server //Remove previous instance if running. 
                    docker run -d --name website-test-server  website
                    
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
            echo 'Delete the running container on Test Server.'
        }
    }
}
