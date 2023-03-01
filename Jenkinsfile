pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker images -a'
                sh '''cd App/v1
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ../..'''
            }
        }
    }
}
