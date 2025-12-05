pipeline {
    agent any

    tools {
        maven 'Maven_3.9.11'
        jdk 'jdk-21'
    }

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
