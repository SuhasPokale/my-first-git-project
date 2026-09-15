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
                sh '''
                    if ! command -v python3 >/dev/null 2>&1; then
                        if command -v sudo >/dev/null 2>&1; then
                            sudo apt-get update
                            sudo apt-get install -y python3 python3-venv python3-pip
                        else
                            echo "python3 is required but not installed on this Jenkins agent."
                            exit 1
                        fi
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