pipeline {
    agent any

    tools {
        // Make sure Maven is installed in Jenkins (Global Tool Configuration)
        maven 'Maven 3.9.11'
        jdk 'JDK 21'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run Maven build from repo root
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Publish to Nexus') {
            steps {
                // Deploy with debug enabled (-X) so you can see if settings.xml is picked up
                sh './mvnw deploy -DskipTests -X'
            }
        }
    }

    post {
        success {
            echo 'Build and Deploy succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
