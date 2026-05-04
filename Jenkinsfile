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
                    mail to: 'haseebgulkhan12@gmail.com',
                         subject: 'Run Tests Stage Completed',
                         body: 'The Run Tests stage has finished. Please check the Jenkins console output for logs.'
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
                    mail to: 'haseebgulkhan12@gmail.com',
                         subject: 'NPM Audit Security Scan Completed',
                         body: 'The NPM Audit security scan stage has finished. Please check the Jenkins console output for vulnerability details.'
                }
            }
        }
    }
}