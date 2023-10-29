pipeline {
    agent any
    environment {
	branchName = sh(script: 'echo $BRANCH_NAME | sed "s#/#-#"', returnStdout: true).trim()
	MY_VARIABLE = sh(script: 'echo $branchName | sed "s/\\.git$//"', returnStdout: true).trim()
	buildNumber = "$BUILD_NUMBER"
	gitCommit = "${GIT_COMMIT[0..6]}"
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
		    echo "The current branch is without script: $MY_VARIABLE"
                   echo "The current branch is without script: $gitCommit"
                   echo "The current build number of the pipeline is: $buildNumber"
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
