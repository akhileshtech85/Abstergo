pipeline {
    agent docker

    environment {
        GIT_REPO = 'https://github.com/edureka-devops/projCert.git'
        DOCKER_IMAGE = 'devopsedu/webapp'
        SLAVE_NODE = 'test-server'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from the Git repository
                git branch: 'master', url: "${GIT_REPO}"
            }
        }

        stage('Provision Test Server') {
            steps {
                // Provision a new test server using Ansible
                script {
                    echo 'ansible-playbook -i inventory/test_server provision_test_server.yml'
                }
            }
        }

        stage('Install Docker on Test Server') {
            steps {
                // Use Ansible to install Docker on the test server
                script {
                    echo 'ansible-playbook -i inventory/test_server install_docker.yml'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image with the PHP application
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Deploy to Test Server') {
            steps {
                // Deploy the Docker container to the test server
                script {
                    sh "docker run -d --name php_app ${DOCKER_IMAGE}"
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests on the deployed application
                script {
                    // Add your testing commands here
                    sh 'curl http://test-server:port/health'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                // If tests pass, deploy to production
                script {
                    sh "docker run -d --name php_app_prod ${DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        failure {
            // Clean up if the build fails
            script {
                sh "docker rm -f php_app || true"
            }
        }
        success {
            // Notify on success
            echo 'Deployment to production was successful!'
        }
    }
}
