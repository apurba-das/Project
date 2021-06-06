pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/apurba-das/Project.git'
             
          }
        }
	  stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

	  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp apurbadas/samplewebapp:latest'               
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
           steps  {			     {
               sh "docker run -d -p 8003:8080 apurbadas/samplewebapp"
 
           }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.20.211 run -d -p 8003:8080 apurbadas/samplewebapp"
 
           }
        }
    }
	}
    
