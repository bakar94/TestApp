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
                sh 'docker image ls'
                sh '''cd App/v1
                    docker image ls
                    docker build -t jenkins-pipeline .
                    docker image ls
                    cd ../..'''
            }
        }
        stage('Start test app') {
         steps {
            sh '''
               docker-compose up -d
               ./scripts/test_container.sh
            '''
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            sh '''
               pytest ./tests/test_sample.py
            '''
         }
      }
      stage('Stop test app') {
         steps {
            sh '''
               docker-compose down
            '''
         }
      }
    }
}
