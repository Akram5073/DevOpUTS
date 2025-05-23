pipeline {
    agent {
        docker {
            image 'python:3.11'
            args '-u'  // output realtime
        }
    }

    environment {
        VENV_DIR = '.venv'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Virtual Env & Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . ${VENV_DIR}/bin/activate
                    pytest
                '''
            }
        }

        // Optional: jalankan Flask app di background selama pipeline berjalan
        stage('Run Flask (optional)') {
            steps {
                sh '''
                    . ${VENV_DIR}/bin/activate
                    nohup flask run --host=0.0.0.0 --port=5000 &
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline selesai.'
        }
        failure {
            echo 'Build gagal!'
        }
        success {
            echo 'Build berhasil!'
        }
    }
}
