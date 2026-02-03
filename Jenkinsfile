pipeline {
    agent any

    tools {
        jdk 'JDK 17'
        maven 'Maven 3.9'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean compile'
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Java CI Pipeline completed successfully!'
        }
        failure {
            echo 'Java CI Pipeline failed!'
        }
    }
}
