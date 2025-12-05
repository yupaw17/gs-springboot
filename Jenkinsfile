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
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Verify Maven Settings') {
            steps {
                sh './mvnw help:effective-settings -X'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                sh './mvnw deploy -DskipTests -X'
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
