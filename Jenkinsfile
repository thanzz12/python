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
                . venv/bin/activate
                pip install -r requirements.txt || echo "flask" > requirements.txt && pip install flask
                '''
            }
        }
        stage('Run Application') {
            steps {
                sh 'python app.py &'
            }
        }
    }
}

