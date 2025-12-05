pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                sh './mvnw deploy -f pom.xml -DskipTests -X'
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
