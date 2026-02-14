pipeline {
    agent any

    tools {
        maven 'M3'   // Name of Maven installation in Jenkins
        jdk 'JDK17'      // Name of JDK installation in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the project...'
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            echo 'Build, test, and package succeeded!'
        }
        failure {
            echo 'Something went wrong...'
        }
    }
}

