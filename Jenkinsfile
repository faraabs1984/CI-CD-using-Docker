pipeline {
  environment {
    imagename = ""
    registryCredential = 'docker_hub_login'
    dockerImage = ''
  }
  agent any
    stages {
      
      
    stage ('GitCheckout') {
            steps {
            echo 'Checking Git repository'
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_key', url: 'https://github.com/faraabs1984/CI-CD-using-Docker.git']]])
            }
        }
    stage ('BuildImage'){
            steps{
                echo 'Building Docker Image'
                sh '''docker build -t webapp .
                      docker tag webapp faraabs/webapp && docker rmi webapp'''
            }
        }
    stage('Push Image') {
      steps{
        script {
          withCredentials([usernameColonPassword(credentialsId: 'docker_hub_login', variable: 'docker')]) {
            sh '''docker push faraabs/webapp:latest && docker rmi faraabs/webapp:latest 
                   '''
            } 
         }
      }
   }
    stage('Deploy Conatiner'){
        steps{
                sh 'docker run --rm -d -p 8000:8080 faraabs/webapp:latest'
            }
    }
  }
}
