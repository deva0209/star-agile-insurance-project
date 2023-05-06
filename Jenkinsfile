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
  }
}
