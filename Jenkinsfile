pipeline {
    agent any
    
    stages {
        stage('Git checkout') {
            steps {
                echo 'We are now checking out the git repository'
                git 'https://github.com/rohith-marigowda/javaProject.git' 
            }
        }
        stage('Fetch Branch Name') {
            steps {
                script {
                    // Access the BRANCH_NAME environment variable
                    def branchName = env.BRANCH_NAME
                    echo "The current branch is: $branchName"
                }
            }
        }
        stage('Test'){
            steps{
                 echo "The current branch is without script: ${env.BRANCH_NAME}"
            }
    }
}
