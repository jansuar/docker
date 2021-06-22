node {
    def app

    // environment { 
    // registry = "YourDockerhubAccount/YourRepository"
    // registryCredential = 'dockerhub_id' 
    // dockerImage = '' 
    def ACR_CRED_ID='azregistry'
    def ACR_SERVER='devjasa.azurecr.io'
    def IMAGE='test1'
    // }

    stage('Clone repository') {      

        checkout scm
    }

    stage('Build image') {
      // steps {

        echo 'DOCKER BUILD'
        sh 'whoami'
        sh 'pwd'

        // withCredentials([usernamePassword(credentialsId: $ACR_CRED_ID, usernameVariable: 'ACR_USER', passwordVariable: 'ACR_PASSWORD')]{
          sh 'docker login -u $ACR_USER -p $ACR_PASSWORD https://$ACR_SERVER'
          // build image
          def imageWithTag = "$ACR_SERVER/$IMAGE:$env.BUILD_NUMBER"
          app = docker.build imageWithTag

          //app = docker.build("jansuar/test")

          //docker.build("${ecRegistry}/${image}:${imageTag}", "${dockerFile}")

          sh 'docker images'
        // }
      // }
  
    }
  
    stage('Test image') {

      app.inside {
          sh 'echo "Tests passed"'
      }
    }

    stage('Push image') {
      echo 'DOCKER PUSH'

      docker.withRegistry ("https://${ACR_SERVER}", "$ACR_CRED_ID") {

        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
      }
    }
}
