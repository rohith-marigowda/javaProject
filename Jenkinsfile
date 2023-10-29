pipeline {
    agent any
    environment {
	branchNameOld = "$BRANCH_NAME"
	def branchName = "env.BRANCH_NAME"
	def modifiedBranchName = '$branchName.replaceAll("/", "-")'
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
                   echo "The current branch is without script: $modifiedBranchName"
                   echo "The current branch is without script: $gitCommit"
                   echo "The current build number of the pipeline is: $buildNumber"
            }
        }
        stage('Fetch Branch Name1') {
             script {
                    def originalBranchName = sh(script: 'echo $BRANCH_NAME', returnStdout: true).trim()
                    def modifiedBranchName = sh(script: 'echo $originalBranchName | sed "s#/#-#"', returnStdout: true).trim()
                    echo "Modified Branch Name: $modifiedBranchName"
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
