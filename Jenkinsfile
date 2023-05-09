pipeline {
    agent any
    stages {
        stage('Check Java & Maven Version') {
            steps {
                sh 'java --version'
		echo "check Maven and Java Version "
		sh 'mvn --version'
            }
        }
	stage('clone git repo') {
	    steps {
		git branch: 'master', url: 'https://github.com/deva0209/star-agile-insurance-project.git'
	    }
        }
	stage('package the project') {
	     steps {
	    	sh 'mvn clean package'
	     }
	}
	stage('Publish HTML reports') {
	     steps {
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
	     }
	}
	stage('build docker image') {
	     steps {
	    	sh 'docker build -t deva0209/insure-me .'
  	     }
	}
	stage('push image to docker hub') {
             steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USER')]) {
                        sh "docker login -u ${env.DOCKERHUB_USER} --password-stdin ${env.DOCKERHUB_PASSWORD}"
                        sh 'docker push deva0209/insure-me:latest'
                }
             }
        }
	/*stage('deploy using ansible') {
	    steps {
		ansiblePlaybook become: true, credentialsId: 'execute-ansible', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-deploy.yml'
	    }
	}*/
    }
}
