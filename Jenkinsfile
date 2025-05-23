pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'development', url: 'https://github.com/Akram5073/DevOpUTS.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Flask App') {
            steps {
                sh '''
                . venv/bin/activate
                nohup python main.py &
                sleep 5
                curl http://127.0.0.1:5000
                '''
            }
        }

        
        stage('Run Tests') {
            steps {
                sh '''
                . venv/bin/activate
                PYTHONPATH=. pytest test_main.py
                '''
            }
        }
    }
}
