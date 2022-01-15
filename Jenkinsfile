pipeline {
    agent any
	
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/faraabs1984/CI-CD-using-Docker.git'
             
          }
        }
	
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t webapp:latest .' 
                sh 'docker tag webapp faraabs/webapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerHUB') {
          sh  'docker push faraabs/webapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 faraabs/webapp:latest"
 
            }
        }
 }
}
    
