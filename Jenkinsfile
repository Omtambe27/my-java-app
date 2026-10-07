pipeline {

    agent any

    tools {
        jdk 'JDK-17'
        maven 'Maven-3.9'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Unit Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    if not exist C:\\tmp mkdir C:\\tmp
                    copy /Y target\\my-java-app-1.0-SNAPSHOT.jar C:\\tmp\\deployed-app.jar
                '''
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
    }
}