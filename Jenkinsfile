pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/SuhasPokale/my-first-git-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                    py -3 -m venv venv
                    call venv\\Scripts\\activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                    call venv\\Scripts\\activate
                    pytest -q
                '''
            }
        }

        stage('Build Completed') {
            steps {
                echo 'Application Built Successfully'
            }
        }
    }
}