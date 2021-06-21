node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
      
      //docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
     //   git '…'
    //    docker.build('myapp').push('latest')
    //}
  
       app = docker.build("jansuar/test")
      //}
    }
  
    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
