pipeline {
    agent any
    environment {
	branchNameOld = "$BRANCH_NAME"
	MODIFIED_BRANCH_NAME = sh(script: 'echo $BRANCH_NAME | sed "s#/#-#"', returnStdout: true).trim()
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
                   echo "The current branch is without script: $MODIFIED_BRANCH_NAME"
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
