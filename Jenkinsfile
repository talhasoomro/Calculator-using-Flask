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

        stage('Verify requirements.txt') {
            steps {
                // Verify that requirements.txt file exists
                script {
                    if (!fileExists('requirements.txt')) {
                        error "requirements.txt not found in the repository."
                    }
                }
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                script {
                    // Check for the virtual environment, create it if it doesn't exist
                    sh 'python3 -m venv $VENV_PATH'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install any dependencies listed in requirements.txt
                sh 'bash -c "source $VENV_PATH/bin/activate && pip install -r requirements.txt"'
            }
        }

        stage('Test') {
            steps {
                // Run your tests here
                echo "Running tests..."
                sh 'bash -c "source $VENV_PATH/bin/activate && pytest"'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy your Flask app
                    echo 'Deploying application...'
                    // Example deployment command, modify as needed
                    // sh 'bash -c "scp -r . user@your_server:/path/to/deploy"'
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
