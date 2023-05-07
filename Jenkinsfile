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
	publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/insur-eme/target', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: 'true'])
	}
  }
    stage('Docker Image Creation') {
        steps {
	sh 'sudo docker build -t deva0209/insure-me:latest .'
	}
    }
        stage('Docker Login') {
            steps {
                input message: 'Please enter your DockerHub credentials', parameters: [
                    string(name: 'DOCKERHUB_USERNAME', defaultValue: '', description: 'DockerHub username'),
                    password(name: 'DOCKERHUB_PASSWORD', defaultValue: '', description: 'DockerHub password')
                ]
                sh """
                    echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin < /dev/tty
                """
	    }
	}
  }
}
