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
                sh 'docker image ls -v $(which docker):/opt/homebrew/bin/docker'
                sh '''cd App/v1
                    docker image ls
                    docker build -t jenkins-pipeline .
                    docker image ls
                    cd ../..'''
            }
        }
    }
}
