pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-nginx .'
        sh 'docker tag my-nginx $DOCKER_NGINX_IMAGE'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run my-nginx nginx -m pytest app/tests/'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
          sh "echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin docker.io"
          sh 'docker push $DOCKER_NGINX_IMAGE'
        }
      }
    }
    
  }

post{
      success{
        mail to: "atchayasara@gmail.com",
             subject: "Build successfull",
             body:"The Build is successfull"
                  
                  
        }
      failure{
        mail  to: "atchayasara@gmail.com",
              subject: "Build failed",
              body:"The Build is failure"
                 
                
      } 
}

}

             
              
  

                 
    
  
    

  

