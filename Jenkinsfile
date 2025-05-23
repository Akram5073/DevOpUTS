pipeline {
    agent {
        docker {
            image 'python:3.10'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'development', url: 'https://github.com/Akram5073/DevOpUTS.git'
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
