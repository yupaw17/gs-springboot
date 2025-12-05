pipeline {
    agent any

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/yupaw17/gs-springboot.git'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh './mvnw clean test'
            }
        }

        stage('Build and Package') {
            steps {
                // Build the JAR file
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Publish to Nexus') {
            steps {
                // Deploy artifact to Nexus (requires distributionManagement in pom.xml)
                sh './mvnw deploy -DskipTests'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Save JAR file in Jenkins
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
