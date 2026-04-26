pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git 'https://github.com/C-MINDA/juice-shop.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t juice-shop .'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running Juice Shop container...'
                sh 'docker run -d -p 3000:3000 --name juice-shop-container juice-shop || true'
            }
        }

        stage('Verify Application') {
            steps {
                echo 'Checking if app is running...'
                sh '''
                    sleep 10
                    curl -I http://localhost:3000 || exit 1
                '''
            }
        }

        stage('Archive Info') {
            steps {
                echo 'Saving build info...'
                sh 'echo "Build successful!" > build.txt'
                archiveArtifacts artifacts: '*.txt'
            }
        }
    }
}