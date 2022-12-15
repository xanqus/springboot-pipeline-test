def mainDir=""
def ecrLoginHelper="docker-credential-ecr-login"
def region="ap-northeast-2"
def ecrUrl="526336633172.dkr.ecr.ap-northeast-2.amazonaws.com"
def repository="pipeline-test"
def deployHost="172.17.0.1"

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
        stage('Build Docker Image by Jib & Push to AWS ECR Repository') {
            steps {
                sh """
                mv ${ecrLoginHelper} /usr/local/bin/
                ./gradlew jib -Djib.to.image=my-springboot-app:latest -Djib.console='plain'
                """
            }
        }
    }
}