pipeline {
    agent any
    stages {
        stage('Cleanup') {
            steps {
                sh 'rm -rf venv'  // Remove any old venv directory
            }
        }
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/thanzz12/python.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                bash -c "source venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt || pip install flask"
                '''
            }
        }
        stage('Run Application') {
            steps {
                sh '''
                pkill -f app.py || true
                bash -c "source venv/bin/activate && nohup python app.py > app.log 2>&1 &"
                '''
            }
        }
    }
    post {
        always {
            sh 'tail -n 20 app.log || true'
        }
    }
}

