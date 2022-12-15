
pipeline {
    agent any

    stages {
        stage('Pull Codes from Github'){
            steps{
                checkout scm
            }
        }
        stage('Build Codes by Gradle') {
            steps {
                sh """
                pwd
                chmod +x gradlew
                ./gradlew clean build
                """
            }
        }
        stage('Build Docker Image by Jib') {
            steps {
                sh """
                docker build -t my-springboot-app:latest .
                """
            }
        }
    }
}