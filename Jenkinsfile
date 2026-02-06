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
                "C:\\Users\\Anjali\\AppData\\Local\\Programs\\Python\\Python311\\python.exe" --version
                "C:\\Users\\Anjali\\AppData\\Local\\Programs\\Python\\Python311\\python.exe" -m venv venv
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
                echo Starting deployment...

                mkdir C:\\deploy 2>Nul
                rmdir /S /Q C:\\deploy\\django-todo 2>Nul

                
                robocopy %WORKSPACE% C: \\deploy\\django-todo /E
                IF %ERROELEVEL% LEQ 3 exit 0
                """
            }
        }
    }
}
