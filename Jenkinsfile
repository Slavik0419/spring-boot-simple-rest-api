pipeline {
    agent {
        docker {
            image 'maven:3.9.9-eclipse-temurin-11'
        }
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }

        stage('Build') {
            steps {
                dir('com.divit.spring-boot-simple-rest-api') {
                    sh 'mvn -B clean package -DskipTests'
                }
            }
        }

        stage('Test') {
            steps {
                dir('com.divit.spring-boot-simple-rest-api') {
                    sh 'mvn -B test'
                }
            }
        }
    }
}
