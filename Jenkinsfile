pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                bat """
                python --version
                python -m venv venv
                """
            }
        }

        stage('Install Dependencies') {
            steps {
                bat """
                venv\\Scripts\\python -m pip install --upgrade pip
                venv\\Scripts\\pip install -r requirements.txt
                """
            }
        }

        stage('Run Migrations') {
            steps {
                bat """
                venv\\Scripts\\python manage.py migrate
                """
            }
        }

        stage('Run Tests') {
            steps {
                bat """
                venv\\Scripts\\python manage.py test
                """
            }
        }
    }
}
