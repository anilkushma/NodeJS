pipeline {
    agent any

    environment {
        // Set environment variables if needed
        NODE_ENV = 'development'
        // Add the path to npm if necessary (adjust as needed)
        PATH = "${env.PATH}:/path/to/node/bin"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure npm is available and install Node.js dependencies
                    sh 'npm --version || { echo "npm not found"; exit 1; }'
                    sh 'npm install'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Start npm in the background and get its PID
                    sh '''
                    npm start &
                    NPM_PID=$!
                    sleep 60
                    kill $NPM_PID
                    '''
                }
            }
        }

        // Add further stages as needed
        // stage('NextStage') {
        //     steps {
        //         // Add further steps here
        //     }
        // }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
        always {
            echo 'Pipeline finished.'
        }
    }
}
