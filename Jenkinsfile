pipeline {
    agent any 
    environment {
        // user_id at dockerhub
        registry = "ezenmin/kiwi_imgbuilder"
        //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = 'ezenmin_dockerhub'
        dockerImage = ''
    }
    
    stages {

    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
    
     // Uploading Docker images into Docker Hub
    stage('Upload Image') {
     steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }

    // Running Docker container, make sure port 8096 is opened in 
    stage('Docker Run') {
     steps{
         script {
            dockerImage.run("-d --name kiwi_jenkins --privileged")
         }
      }
    }
  }
}
