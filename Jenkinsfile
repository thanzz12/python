pipeline {
    agent any
    stages {
        stage('Cleanup') {
            steps {
                // Remove the old virtual environment
                sh 'rm -rf venv'
            }
        }
        stage('Clone Repository') {
            steps {
                // Clone the repository
                git branch: 'main', url: 'https://github.com/thanzz12/python.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Create a new virtual environment and install dependencies
                sh '''
                # Create the virtual environment
                python3 -m venv venv

                # Ensure correct permissions on the virtual environment
                chmod -R 755 venv

                # Use bash to activate the virtual environment and install dependencies
                bash -c "source venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt || pip install flask"
                '''
            }
        }
        stage('Run Application') {
            steps {
                // Ensure no other app instances are running
                sh '''
                pkill -f app.py || true

                # Use bash to activate virtual environment and start the application
                bash -c "source venv/bin/activate && nohup python app.py > app.log 2>&1 &"
                '''
            }
        }
    }
    post {
        always {
            // Tail the logs to get the last 20 lines
            sh 'tail -n 20 app.log || true'
        }
    }
}

