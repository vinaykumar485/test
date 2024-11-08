pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "simple-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository (you can configure the repository later)
                git 'https://github.com/vinaykumar485/test.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container
                    sh 'docker run -d -p 3000:3000 ${DOCKER_IMAGE}'
                }
            }
        }

        stage('Test Application') {
            steps {
                script {
                    // Verify the app is running
                    sh 'curl http://localhost:3000'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Clean up: Stop and remove the container
                    sh 'docker ps -q | xargs docker stop'
                    sh 'docker ps -a -q | xargs docker rm'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images and containers
            sh 'docker system prune -f'
        }
    }
}

      
