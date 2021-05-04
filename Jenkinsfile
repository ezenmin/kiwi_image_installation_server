pipeline {
    agent any
    environment {
        // user_id at dockerhub
        registry = "ezenmin/kiwing_imgbuilder4"
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

    // Running image builidng command
    stage('kiwi-ng command') {
     steps{
         script {
            docker.image('ezenmin/kiwing_imgbuilder4').withRun("-i -u 0:0 --name kiwing_jenkins4 --privileged --net=host --device-cgroup-rule='b 7:* rmw' -v /home/ericsson/:/root/local_repositories"){
               sh 'kiwi-ng --debug --profile=VMWare --type oem system build --description /root/kiwi-descriptions/samples --target-dir /root/local_repositories/docker_image_output/sampleimage_jenkins'
            }
         }
      }
    }
  }
}
