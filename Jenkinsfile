pipeline {
    agent any

    environment {
        VENV_DIR = '.venv'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'development', url: 'https://github.com/Akram5073/DevOpUTS.git'
            }
        }

        stage('Setup Virtual Env') {
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
                    pytest tests/ --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Run Flask (optional preview)') {
            when {
                expression { return false } // ubah jadi true jika ingin coba run Flask
            }
            steps {
                sh '''
                    . $VENV_DIR/bin/activate
                    python app/main.py &
                    sleep 5
                    curl -i http://localhost:5000
                    kill $(lsof -t -i:5000)
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
