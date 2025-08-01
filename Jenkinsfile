pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'development', url: 'https://github.com/Akram5073/DevOpUTS.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv $VENV_DIR
                    . $VENV_DIR/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . $VENV_DIR/bin/activate
                    pytest test_main.py --junitxml=results.xml
                '''
            }
            post {
                always {
                    junit 'results.xml'
                }
            }
        }
    }
}
