pipeline {
  agent any
	
  tools {
      maven 'M2_HOME'
    }
  stages {
    
    stage('Checkout') {
       steps {
         echo 'Checkout the code from GitRepo'
         git  'https://github.com/deva0209/star-agile-insurance-project.git'
       }
       }
    stage('Build the Application'){
       steps {
	       echo "Cleaning... Compiling...Testing... Packaging..."
        	sh 'mvn clean package'
       }
    }
    stage('Publish Reports') {
        steps {
	publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/insure-me/target', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: 'true'])
	}
    }
	  stage('Docker Login') {
            steps {
                script {
                    def userInput = input(
                        message: 'Enter DockerHub credentials',
                        parameters: [
                            [$class: 'StringParameterDefinition', defaultValue: 'deva0209', description: 'Enter DockerHub username', name: 'DOCKERHUB_USERNAME'],
                            [$class: 'PasswordParameterDefinition', description: 'Enter DockerHub password', name: 'DOCKERHUB_PASSWORD']
                        ]
                    )
                    sh 'echo $userInput.DOCKERHUB_PASSWORD | docker login -u $userInput.DOCKERHUB_USERNAME --password-stdin'
                }
            }
        }
        stage('Build and Push Image') {
            steps {
                sh """
                    docker build -t insure-me .
                    docker tag insure-me deva0209/insure-me
                    docker push deva0209/insure-me
                """
            }
        }
  }
}
