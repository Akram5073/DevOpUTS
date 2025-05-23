pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/username/flask-ci-demo.git' // Ganti dengan repo kamu
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest tests/ --maxfail=1 --disable-warnings -q'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
