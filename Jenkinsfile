pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                sh 'docker tag nginxtest sksumit1999/dockertask:tagfr'
               
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push sksumit1999/dockertask:tagfr'
         
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 sksumit1999/dockertask"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.23.148.54 run -d -p 4001:80 sksumit1999/dockertask"
 
            }
        }
    }
}
