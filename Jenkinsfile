pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Application...'
                // simpler simulation of a build
                sh 'sleep 2' 
            }
        }
        stage('Test') {
            steps {
                echo 'Running Tests...'
                // REMOVED 'exit 1' so it passes now!
                sh 'sleep 2'
            }
        }
        
        // This stage will PAUSE the pipeline until you click "Proceed"
        stage('Approval') {
            steps {
                input message: 'Tests passed. Deploy to Production?', ok: 'Yes, Deploy!'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying to Production Server...'
            }
        }
    }
    
    post {
        failure {
            emailext (
                subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: "Check console: ${env.BUILD_URL}",
                to: "adityazade69@gmail.com" // Ensure this matches your admin email
            )
        }
        success {
             // Optional: Send an email when deployment is successful
             emailext (
                subject: "DEPLOYED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: "The application has been successfully deployed.",
                to: "adityazade69@gmail.com"
            )
        }
    }
}
