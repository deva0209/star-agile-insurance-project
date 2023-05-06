pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/deva0209/star-agile-insurance-project.git'
            }
        }
        stage('Build') {
            steps {
                withMaven(maven: 'maven-3.8.1') {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Test') {
            steps {
                withMaven(maven: 'maven-3.8.1') {
                    sh 'mvn test'
                }
            }
        }
    }
}
