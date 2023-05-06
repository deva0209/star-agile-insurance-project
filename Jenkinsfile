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
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
