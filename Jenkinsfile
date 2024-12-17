pipeline {
    agent any

    environment {
        NODE_VERSION = '16' // Specify the Node.js version
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Setup Node.js') {
            steps {
                echo 'Setting up Node.js environment...'
                script {
                    // Use Node.js plugin or install Node.js manually
                    sh """
                    curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION}.x | sudo -E bash -
                    sudo apt-get install -y nodejs
                    node -v
                    npm -v
                    """
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing project dependencies...'
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }

        stage('Deploy') {
            when {
                branch 'main' // Deploy only for the main branch
            }
            steps {
                echo 'Deploying application...'
                // Replace this with actual deployment commands
                sh """
                echo "Deploying to production server..."
                """
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'rm -rf node_modules'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
