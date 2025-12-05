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
                sh './mvnw deploy -DskipTests -DaltDeploymentRepository=nexus-snapshots::default::http://localhost:8081/repository/maven-snapshots/ -X'
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
