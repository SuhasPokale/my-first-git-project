pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/SuhasPokale/my-first-git-project.git'
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: env.REPO_URL
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    if ! command -v python3 >/dev/null 2>&1; then
                        apt-get update
                        apt-get install -y python3 python3-venv python3-pip
                    fi

                    python3 -m venv venv
                    . venv/bin/activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . venv/bin/activate
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