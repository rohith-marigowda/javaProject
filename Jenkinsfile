pipeline {
    agent any
    environment {
	branchName = sh(script: 'echo $BRANCH_NAME | sed "s#/#-#"', returnStdout: true).trim()
	buildNumber = "$BUILD_NUMBER"
	gitCommit = "${GIT_COMMIT[0..6]}"
	dockerImage = "878226295837.dkr.ecr.ap-south-1.amazonaws.com/javaproject-cicd:${branchName}-${gitCommit}-${buildNumber}"
	ecrURL = "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 878226295837.dkr.ecr.ap-south-1.amazonaws.com"
}
    stages {
        stage('Git checkout') {
            steps {
                echo 'We are now checking out the git repository'
                git 'https://github.com/rohith-marigowda/javaProject.git' 
            }
        }
         stage('Fetch Branch Name') {
            steps {
                   echo "The current branch is without script: $branchName"
                   echo "The git commid id is : $gitCommit"
                   echo "The current build number of the pipeline is: $buildNumber"
		   echo "docker image is : $dockerImage"
            }	 
        }
	    
        stage('masterBranch') {
            when {
                branch "master"
            }
            steps {
                echo 'Trigger the test cases when code is pushed to master branch' 
            }
        }
        stage('releaseBranch') {
            when {
                branch "release/*"
            }
            steps {
                echo 'Trigger the test cases when code is pushed to release branch'
            }
        }
    }
}
