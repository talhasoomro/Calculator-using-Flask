pipeline {
    agent any

    environment {
        VENV_PATH = 'myprojectenv'
        FLASK_APP = 'app.py' // Assuming your main Flask app is named app.py
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git url: 'https://github.com/talhasoomro/Calculator-using-Flask', branch: 'master'
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                script {
                    // Check for the virtual environment, create it if it doesn't exist
                    sh 'python3 -m venv $VENV_PATH'
                    // Activate the virtual environment
                    sh '. $VENV_PATH/bin/activate'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install any dependencies listed in requirements.txt
                sh '. $VENV_PATH/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                // Run your tests here
                echo "Running tests..."
                sh '. $VENV_PATH/bin/activate && pytest'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy your Flask app
                    echo 'Deploying application...'
                    // Example deployment command, modify as needed
                    // sh 'scp -r . user@your_server:/path/to/deploy'
                }
            }
        }
    }

    post {
        always {
            // Clean up after the pipeline runs
            echo 'Cleaning up...'
            sh 'rm -rf ${VENV_PATH}'
        }
    }
}
