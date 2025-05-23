pipeline {
    agent {
        docker {
            image 'python:3.11'
            args '-u'  // supaya output realtime (optional)
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

        stage('Setup Virtual Env') {
            steps {
                sh 'python3 -m venv ${VENV_DIR}'
                sh '''
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
                    # Misal kamu pakai pytest, sesuaikan jika pakai test framework lain
                    pytest
                '''
            }
        }

        stage('Run Flask (optional preview)') {
            steps {
                script {
                    // Kalau kamu mau jalankan flask untuk preview,
                    // ini contoh menjalankan Flask di background selama pipeline berjalan (opsional)
                    sh '''
                        . ${VENV_DIR}/bin/activate
                        nohup flask run --host=0.0.0.0 --port=5000 &
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo 'Build failed!'
        }
        success {
            echo 'Build succeeded!'
        }
    }
}
