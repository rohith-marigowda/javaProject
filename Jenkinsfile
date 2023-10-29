pipeline {
    agent any
    environment {
	branchName = env.BRANCH_NAME
}
    stages {
        stage('Git checkout') {
            steps {
                echo 'We are now checking out the git repository'
                git 'https://github.com/rohith-marigowda/javaProject.git' 
            }
        }
        stage('test') {
          sh 'echo "The current branch is: $branchName"'
        }
    }
}
