pipeline {
    agent any
    stages {
        stage('Git checkout') {
            steps {
                echo 'We are now checking out the git repository'
                git 'https://github.com/rohith-marigowda/javaProject.git' 
            }
        }
        stage('test') {
          sh 'echo Branch Name: $BRANCH_NAME'
        }
    }
}
