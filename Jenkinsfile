pipeline {
    agent any

    environment {
	branchName = "$BRANCH_NAME"
	gitCommit = "${GIT_COMMIT[0..6]}"
	buildNumber = "$BUILD_NUMBER"
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
                   echo "The current branch is without script: $gitCommit"
                   echo "The current build number of the pipeline is: $buildNumber"
            }
        }
        
    }
}
