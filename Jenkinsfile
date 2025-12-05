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
                // Use Maven wrapper from repo root
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                // Deploy with debug enabled to trace settings.xml and repository config
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
