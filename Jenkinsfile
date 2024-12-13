pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the Git repository
                git branch: 'main', url: 'https://github.com/thanzz12/python.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                # Clean up old virtual environment if it exists
                rm -rf venv
                
                # Create a new virtual environment
                python3 -m venv venv
                
                # Activate the virtual environment and install dependencies
                bash -c "source venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt || pip install flask"
                '''
            }
        }
        stage('Run Application') {
            steps {
                sh '''
                # Stop any previously running application
                pkill -f app.py || true
                
                # Run the application in the background
                bash -c "source venv/bin/activate && nohup python app.py > app.log 2>&1 &"
                '''
            }
        }
    }
    post {
        always {
            // Print the last few lines of the log for debugging
            sh 'tail -n 20 app.log || true'
        }
    }
}

