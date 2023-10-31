pipeline {
    agent {label 'slave3'}
    environment {
	AWS_REGION = "ap-south-1"
	AWS_ECR_URL = "878226295837.dkr.ecr.ap-south-1.amazonaws.com"
	AWS_ECR_REPONAME = "$AWS_ECR_URL/dockerassignment-cicd"
	DOCKER_IMAGE_MASTER = "$AWS_ECR_REPONAME:${BRANCH_NAME}"
	DOCKER_IMAGE_LATEST = "$AWS_ECR_REPONAME:latest"
	
	ECR_LOGIN = "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin ${AWS_ECR_URL}"
}
    stages {
        stage('Git checkout') {
            steps {
                echo 'We are now checking out the git repository'
                git 'https://github.com/rohith-marigowda/javaProject.git'
            }
        }

	 stage('Run Unit and Integration tests'){
  	    steps {
		echo 'In this step run unit and integration tests'
	    }
	 }
	    
         stage('Build docker image') {
            steps {
		sh 'docker build --tag ${DOCKER_IMAGE_MASTER} .'
		sh 'docker build --tag ${DOCKER_IMAGE_LATEST} .'
            }	 
        }
	    
        stage('docker image push to ECR') {
            steps {
		    script{
			sh "$ECR_LOGIN"
			sh 'docker push ${DOCKER_IMAGE_MASTER}'
			sh 'docker push ${DOCKER_IMAGE_LATEST}'
		    }
            }
        }
	    
        stage('deploy') {
            steps {
                sh 'docker run -d -p 9095:8080 ${DOCKER_IMAGE_MASTER}'	
            }
        }
    }
}
