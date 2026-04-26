pipeline {
    agent any

    options {
        // Keeps the console output clean and limits the number of old builds
        buildDiscarder(logRotator(numToKeepStr: '3'))
        timeout(time: 1, unit: 'HOURS') 
    }

    stages {
        stage('🛠️ Build Image') {
            steps {
                echo 'Building the OWASP Juice Shop Docker image...'
                // Based on Project Requirement [3], we use the Docker version
                sh 'docker build -t juice-shop:latest .'
            }
        }

        stage('🔍 SAST (Static Analysis)') {
            steps {
                echo 'Running Static Application Security Testing...'
                /* 
                   TEAM MEMBER 4 (SAST Specialist) ACTION:
                   Insert SonarQube or ESLint security scan commands here.
                   Requirement: Identify 2 OWASP Top 10 vulnerabilities [4].
                */
                echo 'SAST Scan Placeholder - To be implemented by SAST Specialist.'
            }
        }

        stage('📦 SCA (Dependency Scan)') {
            steps {
                echo 'Running Software Composition Analysis...'
                /* 
                   TEAM MEMBER 3 (SCA Specialist) ACTION:
                   Insert OWASP Dependency-Check or Retire.js commands here.
                   Requirement: SCA should trigger during the build phase [2, 5].
                */
                echo 'SCA Scan Placeholder - To be implemented by SCA Specialist.'
            }
        }

        stage('🚀 Deploy to Staging') {
            steps {
                echo 'Deploying application for dynamic testing...'
                // Spin up the container so the DAST tool has a live target to scan
                sh 'docker run -d --name juice-shop-staging -p 3000:3000 juice-shop:latest'
                // Give the app a few seconds to fully start up
                sleep 20
            }
        }

        stage('🛡️ DAST (Dynamic Analysis)') {
            steps {
                echo 'Running Dynamic Application Security Testing...'
                /* 
                   TEAM MEMBER 2 (DAST Specialist) ACTION:
                   Insert OWASP ZAP or Nuclei commands here.
                   Requirement: Scan the live app at http://localhost:3000 [2, 6].
                */
                echo 'DAST Scan Placeholder - To be implemented by DAST Specialist.'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up environment...'
            // Stop and remove the test container to free up resources
            // sh 'docker stop juice-shop-staging || true'
            // sh 'docker rm juice-shop-staging || true'
        }
        success {
            echo 'Pipeline completed successfully! Security scans are ready for review.'
        }
        failure {
            echo 'Pipeline failed. Check the logs for vulnerability blocks or build errors.'
        }
    }
}