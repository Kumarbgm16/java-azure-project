pipeline {
    agent any
    stages {
        stage('git clone') {
            steps {
               git 'https://github.com/coderepo2891/java-azure-project-forked.git'
            }
        }
        stage('maven package') {
            steps {
               sh 'mvn clean package'
            }
        }
		stage('create the docker image') {
            steps {
            sh 'sudo docker build -t aqibdocker2891/web-java-awsb60:v1 .'
            }
        }
           stage('docker push ') {
     steps {
     withCredentials([string(credentialsId: 'DOCKER_HUB_PWD', variable: 'DOCKER_HUB_PASS_CODE')])  {
    // some block
        sh "sudo docker login -u aqibdocker2891 -p $DOCKER_HUB_PASS_CODE"
        }
        sh "sudo docker push aqibdocker2891/web-java-awsb60:v1"
        }
        } 	
  stage('Deploy to docker Env') {
    steps {
   sh "sudo docker rm -f mysecureapp" 
    sh "sudo docker run -itd --name mysecureapp -p 9000:8080 aqibdocker2891/web-java-awsb60:v1" 

}
}
    } 
    }
	
	
	
