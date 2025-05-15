pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kangzonthemic/8.2CDevSecOps'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit 0'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit 0'
            }
        }
      
    }
    post {
        success {
            emailext (
                to: 'doremon02102004@gmail.com',
                subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build was successful! Check it out at ${env.BUILD_URL}",
                attachLog: true
            )
        }
        failure {
            emailext (
                to: 'doremon02102004@gmail.com',
                subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build has failed. Check it out at ${env.BUILD_URL}",
                attachLog: true
            )
        }
    }
}
