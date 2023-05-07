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
    withCredentials([usernamePassword(credentialsId: 'dockerhubpsswd', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
      withEnv(['DOCKER_REGISTRY=registry.hub.docker.com', 'DOCKER_CLI_EXPERIMENTAL=enabled']) {
        sh '''
          echo "$DOCKER_PASSWORD" | docker login --username $DOCKER_USERNAME --password-stdin $DOCKER_REGISTRY
        '''
      }
    }
  }
}
  }
}
