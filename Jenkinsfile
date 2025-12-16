pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    options {
        timestamps()
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
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
            post {
                always {
                    // Якщо в проєкті є тести — Jenkins підхопить звіт.
                    junit allowEmptyResults: true, testResults: 'com.divit.spring-boot-simple-rest-api/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Archive artifact (CD)') {
            steps {
                dir('com.divit.spring-boot-simple-rest-api') {
                    // Артефакт розгортання (JAR) для 2.3–2.4
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }
    }

    post {
        always {
            // На випадок якщо буде додано логування/звіти
            archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
        }
    }
}
