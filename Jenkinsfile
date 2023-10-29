pipeline {
    agent slave3
    environment {
	branchName = sh(script: 'echo $BRANCH_NAME | sed "s#/#-#"', returnStdout: true).trim()
	buildNumber = "$BUILD_NUMBER"
	gitCommit = "${GIT_COMMIT[0..6]}"
	dockerImage = "878226295837.dkr.ecr.ap-south-1.amazonaws.com/dockerassignment-cicd:${branchName}-${gitCommit}-${buildNumber}"
	ecrURL = "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 878226295837.dkr.ecr.ap-south-1.amazonaws.com"
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
		sh 'docker build --tag ${dockerImage}'
            }	 
        }
	    
        stage('docker image push to ECR') {
            steps {
                sh '$ecrURL'
		sh 'docker push ${dockerImage}'
            }
        }
        stage('deploy') {
            steps {
                sh 'docker run -it -p 9095:8080 ${dockerImage}'	
            }
        }
    }
}
