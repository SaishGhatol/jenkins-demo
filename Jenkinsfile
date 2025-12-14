pipeline {
    agent any

    // 1. PARAMETERS: These appear when you click "Build with Parameters"
    parameters {
        choice(name: 'DEPLOY_ENV', choices: ['Staging', 'Production'], description: 'Where should we deploy?')
        booleanParam(name: 'SKIP_TESTS', defaultValue: false, description: 'Check to skip unit tests (Not recommended!)')
    }

    stages {
        stage('Initialize') {
            steps {
                // 2. CLEANUP: Start with a fresh folder
                cleanWs() 
                echo "Starting build for environment: ${params.DEPLOY_ENV}"
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling...'
                // Simulate creating a real file (The "Artifact")
                sh 'echo "Application Version 1.0" > app-release.txt'
                sh 'date >> app-release.txt'
            }
        }

        stage('Test') {
            // CONDITIONAL: Only run if SKIP_TESTS is unchecked
            when {
                expression { return params.SKIP_TESTS == false }
            }
            steps {
                echo 'Running Unit Tests...'
                sh 'sleep 2' // Simulate work
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.DEPLOY_ENV}..."
                
                script {
                    if (params.DEPLOY_ENV == 'Production') {
                        // Double check for Production
                        input message: 'Are you sure you want to deploy to PROD?', ok: 'Yes, Go!'
                    }
                }
            }
        }
    }

    post {
        success {
            // 3. ARCHIVE: Save the 'app-release.txt' file so we can download it from the UI
            archiveArtifacts artifacts: 'app-release.txt', followSymlinks: false
            
            echo "Build Successful! Artifacts archived."
        }
    }
}
