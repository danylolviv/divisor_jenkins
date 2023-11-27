pipeline {
    agent any
     triggers { // Corrected from 'trigger' to 'triggers'
            pollSCM('H/5 * * * *') // Replace with your cron expression
        }
    stages {
        stage("Build") {
            steps {
                echo "Yay we run"
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
                // Define delivery steps here
                echo "Delivering the application"
            }
        }
    }
}
