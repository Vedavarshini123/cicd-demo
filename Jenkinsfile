pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "vedavarshini123/cicd-demo"
    }

    tools {
        jdk 'JDK21'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/Vedavarshini123/cicd-demo.git'
            }
        }

        stage('Build Application') {
            steps {
                bat 'mvnw.cmd clean package'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'mvnw.cmd test'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Push Docker Image') {
            steps {

                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push %DOCKER_IMAGE%'
                }
            }
        }
    }
}