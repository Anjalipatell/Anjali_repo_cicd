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
                bat 'python -m venv venv'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                call venv\\Scripts\\activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Migrations') {
            steps {
                bat '''
                call venv\\Scripts\\activate
                python manage.py migrate
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                call venv\\Scripts\\activate
                python manage.py test
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                bat '''
                echo Deploying application...

                mkdir C:\\deploy 2>NUL
                rmdir /S /Q C:\\deploy\\django-todo 2>NUL

                robocopy %WORKSPACE% C:\\deploy\\django-todo /E
                IF %ERRORLEVEL% LEQ 3 exit 0
                '''
            }
        }
    }
}
