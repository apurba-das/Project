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
              
                sh 'docker build -t privaterepo1:latest .' 
                sh 'docker tag privaterepo1 apurba21/privaterepo1:latest'               
          }
        }
	 
   	stage('Publish image to Private repository in Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push apurba21/privaterepo1:latest'
        }                  
          }
        }
     
     
	stage('Run Docker container on Jenkins Agent') {
             
           steps  {			     {
               sh "docker run -d -p 8003:8080 apurba21/privaterepo1"
 
           }
        }
	stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.20.211 run -d -p 8003:8080 apurba21/privaterepo1"
 
           }
        }
    }
	}
    
