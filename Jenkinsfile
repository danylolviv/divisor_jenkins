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
        stage("Preparation") {
            steps {
                script {
                    sh 'ls'
                }
            }
        }
        stage('Build') {
            steps {
                dir('DivisorCounter-b02') {
                    // Run Docker Compose build command
                    sh 'docker compose build'
                }
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
                    dir('DivisorCounter-b02') {
                        // Run Docker Compose build command
                        echo 'Deploy to local environment'
                    }
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