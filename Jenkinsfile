pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/sowmiya1005/CI-CD-using-Docker.git'
             
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
                sh 'docker tag samplewebapp localhost:5000/samplewebapp:latest'
                sh 'docker tag samplewebapp localhost:5000/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
          sh  'docker push localhost:5000/samplewebapp:latest'
          sh  'docker push localhost:5000/samplewebapp:$BUILD_NUMBER' 
        
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 localhost/samplewebapp:$BUILD_NUMBER"
 
            }
        }

             


 
    }
	}
    
