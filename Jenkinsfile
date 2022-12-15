
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
        stage('Build Docker') {
            steps {
                sh """
                docker build -t my-springboot-app:latest .
                """
            }
        }

          stage('Docker run') {
              agent any
              steps {
                  sh 'docker ps -f name=my-springboot-app -q | xargs --no-run-if-empty docker container stop'
                  sh 'docker container ls -a -f name=my-springboot-app -q | xargs -r docker container rm'
                  sh 'docker images --no-trunc --all --quiet --filter="dangling=true" | xargs --no-run-if-empty docker rmi'
                  sh 'docker run -d --name my-springboot-app-dev -p 8091:8234 --net elk__1_default my-springboot-app:latest'
              }
          }
    }
}