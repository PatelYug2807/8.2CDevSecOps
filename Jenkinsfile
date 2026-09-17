pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PatelYug2807/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test | tee test-log.txt || true'
            }
            post {
                always {
                    emailext(
                        subject: 'Run Tests -  - Build #',
                        body: 'Test stage completed with status: . See attached log.',
                        to: 'toxicgaming2807@gmail.com',
                        attachmentsPattern: 'test-log.txt'
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
                sh 'npm audit | tee audit-log.txt || true'
            }
            post {
                always {
                    emailext(
                        subject: 'Security Scan -  - Build #',
                        body: 'NPM audit stage completed with status: . See attached log.',
                        to: 'toxicgaming2807@gmail.com',
                        attachmentsPattern: 'audit-log.txt'
                    )
                }
            }
        }
    }
}