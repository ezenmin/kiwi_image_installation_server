pipeline {
    agent any 
    environment {
        // user_id at dockerhub
        registry = "ezenmin/kiwing_imgbuilder3"
        //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = 'ezenmin_cred'
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
            dockerImage.run("-i --name kiwing_jenkins3 --privileged --net=host --device-cgroup-rule='b 7:* rmw' -v /home/ericsson/:/root/local_repositories ")
         }
      }
    }
  }
}
