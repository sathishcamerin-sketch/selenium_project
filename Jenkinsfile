pipeline {
    agent any 

    // Trigger pipeline automatically when changes are pushed to GitHub
    triggers {
        githubPush()
    }

    environment {
        // Example: Referencing a credential stored in Jenkins
        DB_CREDENTIALS = credentials('my-database-credentials-id')
    }

    stages {
        stage('Checkout') {
            steps {
                // Clones the GitHub repository automatically if configured via SCM
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                // For Node.js: sh 'npm install && npm run build'
                //For Java/Maven: sh './mvnw clean package'
                // For Python: sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                 //sh 'npm test' or sh './mvnw test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }

    // Post-execution blocks to handle notifications or cleanup
    post {
        always {
            echo 'Pipeline has finished execution.'
            cleanWs() // Cleans the workspace directory after the run
        }
        success {
            echo 'Build succeeded! Sending notification...'
        }
        failure {
            echo 'Build failed! Check the console output.'
        }
    }
}
