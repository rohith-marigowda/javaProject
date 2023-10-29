pipeline {
    agent any
    environment {
	branchName = sh(script: 'echo $BRANCH_NAME | sed "s#/#-#"', returnStdout: true).trim()
	repoNameOld = sh(script: 'echo $GIT_URL | sed -nE "s|.*/(.*)(\\.git)?$|\\1|p"', returnStdout: true).trim()
	repositoryName = sh(script: 'echo $BRANCH_NAME | sed "s#.git$##" | xargs -n 1 basename', returnStdout: true).trim()
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
		    echo "The current branch is without script: $repositoryName"
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
