pipeline {
    agent any
    environment {
        // Define environment variables if needed
        DOCKER_IMAGE_TAG = "latest"
        // Assuming Docker Compose is installed at this path; adjust if necessary
        PATH = "/usr/local/bin:$PATH"
    }
    triggers {
        pollSCM('H/5 * * * *')
    }
    stages {
        stage("Build") {
            steps {
                script {
                    // Building Docker images
                    sh 'docker build -t cache-service:${DOCKER_IMAGE_TAG} ./CacheService'
                    sh 'docker build -t divisor-counter:${DOCKER_IMAGE_TAG} ./DivisorCounter'
                }
                echo "Docker Images Built"
            }
        }
        stage("Test") {
            steps {
                // Define test steps here
                echo "Running tests"
            }
        }
        stage("Deliver") {
            steps {
                script {
                    // Running Docker containers
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
                echo "Application Delivered and Running in Docker"
            }
        }
    }
    post {
        always {
            // Clean up after pipeline completion
            echo "Cleaning up"
            sh 'docker-compose -f docker-compose.yml down || true' // Ignore errors in cleanup
        }
    }
}