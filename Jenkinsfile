pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // This command simulates a failure!
                // Remove 'exit 1' to make the build pass.
                sh 'exit 1' 
            }
        }
    }
    
    post {
        failure {
            emailext (
                subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>BUILD FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                         <p>Check console output at: <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>""",
                to: "saishghatol094@gmail.com"  // CHANGE THIS to your actual email
            )
        }
        success {
            echo 'Build succeeded. No email needed.'
        }
    }
}
