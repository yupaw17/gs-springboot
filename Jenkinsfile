pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvnw.cmd clean package -DskipTests'
            }
        }

        stage('Verify Maven Settings') {
            steps {
                bat 'mvnw.cmd help:effective-settings -X'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                bat 'mvnw.cmd deploy -DskipTests -X'
            }
        }
    }

    post {
        success {
            echo '✅ Build and deploy succeeded!'
        }
        failure {
            echo '❌ Build failed. Check console output for Maven errors.'
        }
    }
}
