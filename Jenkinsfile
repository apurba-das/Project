pipeline {
    agent {
           label "Slave1"
         }
   tools
    {
       maven "Maven"
    }
 stages {
	 
 	stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
	 stage('unit test') {
	       steps {
		       sh "mvn test"
	  	       }
	       }
	stage('Docker Build and Tag') {
           steps {
              
                sh 'sudo docker build -t privaterepo1:latest .' 
                sh 'sudo docker tag privaterepo1 apurba21/privaterepo1:latest'               
          }
        }
	 
   	stage('Publish image to Private repository in Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'sudo docker push apurba21/privaterepo1:latest'
        }                  
          }
        }
     
     
	stage('Run Docker container on Jenkins Agent') {
             
           steps  {			     
               sh "sudo docker run -d -p 8003:8080 apurba21/privaterepo1"
 
           }
        }
	stage('Run Docker container on remote hosts') {
             
            steps {
                sh "sudo docker -H ssh://jenkins@172.31.89.123 run -d -p 8003:8080 apurba21/privaterepo1"
 
           }
        }
    }
	}
    
