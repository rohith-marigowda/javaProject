pipeline {
    agent any

    environment {
	gitCommit = $(echo $GIT_COMMIT | cut -c 1-7)
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
                   echo "The current branch is without script: ${env.BRANCH_NAME}"
                   echo "The current branch is without script: $gitCommit"
                   echo "The current build number of the pipeline is: ${env.BUILD_NUMBER}"
            }
        }
        
    }
}
