pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/thanzz12/python.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                # Use bash to activate the virtual environment
                bash -c "source venv/bin/activate && pip install -r requirements.txt || pip install flask"
                '''
            }
        }
        stage('Run Application') {
            steps {
                sh '''
                # Run the application in the background with nohup to avoid blocking Jenkins
                nohup python app.py &
                '''
            }
        }
    }
}

