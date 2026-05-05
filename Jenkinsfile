pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Haseeb578/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
            post {
                always {
                    emailext(
                        to: 'haseebgulkhan12@gmail.com',
                        subject: "Run Tests Stage - ${currentBuild.currentResult}",
                        body: "Run Tests stage completed with status: ${currentBuild.currentResult}. The Jenkins log is attached.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
            post {
                always {
                    emailext(
                        to: 'haseebgulkhan12@gmail.com',
                        subject: "NPM Audit Stage - ${currentBuild.currentResult}",
                        body: "NPM Audit security scan completed with status: ${currentBuild.currentResult}. The Jenkins log is attached.",
                        attachLog: true
                    )
                }
            }
        }
    }
}