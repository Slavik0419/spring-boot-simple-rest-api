pipeline {
    agent any

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
