pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "simple-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository (you can configure the repository later)
                git 'https://github.com/your-username/simple-app.git'
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
                    // Add a wait time to ensure the app has time to start
                    sleep 5  // wait for the app to start

                    // Test the application is running by sending a GET request to the app
                    def response = sh(script: 'curl -s -o /dev/null -w "%{http_code}" http://localhost:3000', returnStdout: true).trim()

                    // Check if the response is 200 (OK)
                    if (response == '200') {
                        echo "Application is running correctly."
                    } else {
                        error "Application did not respond as expected. HTTP Response Code: ${response}"
                    }
                }
            }
        }
    }
}
