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
                py --version
                py -m venv venv
                """
            }
        }

        stage('Install Dependencies') {
            steps {
                bat """
                venv\\Scripts\\activate
                pip install --upgrade pip
                pip install -r requirements.txt
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
        stage('Deploy Application') {
            steps {
                bat """
                if not exist C:\\deploy mkdir C:\\deploy
                xcopy /E /Y %WORKSPACE% C: \\deploy\\django-todo
                """
            }
        }
    }
}
