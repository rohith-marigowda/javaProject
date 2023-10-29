pipeline {
    agent {label 'slave3'}
    environment {
	    
	BRANCH-NAME = sh(script: 'echo $BRANCH_NAME | sed "s#/#-#"', returnStdout: true).trim()
	GIT-COMMIT = "${GIT_COMMIT[0..6]}"
	DOCKER_IMAGE = "878226295837.dkr.ecr.ap-south-1.amazonaws.com/dockerassignment-cicd:${BRANCH-NAME}-${GIT-COMMIT}-${BUILD_NUMBER}"
	AWS_REGION = "ap-south-1"
	AWS_ECR_REPONAME = "878226295837.dkr.ecr.ap-south-1.amazonaws.com"
	ECR_LOGIN = "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin ${AWS_ECR_REPONAME}"
}
    stages {
        stage('Git checkout') {
            steps {
                echo 'We are now checking out the git repository'
                git 'https://github.com/rohith-marigowda/javaProject.git' 
            }
        }
         stage('Build docker image') {
            steps {
		sh 'docker build --tag ${DOCKER_IMAGE} .'
            }	 
        }
	    
        stage('docker image push to ECR') {
            steps {
		    script{
			sh "$ECR_LOGIN"
			sh 'docker push ${DOCKER_IMAGE}'    
		    }
            }
        }
	    
        stage('deploy') {
            steps {
                sh 'docker run -d -p 9095:8080 ${DOCKER_IMAGE}'	
            }
        }
    }
}
