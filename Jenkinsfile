pipeline {
    agent any
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    
    stages {
        
        stage('Test') {
        agent {
          dockerfile {
            filename "productpage/Dockerfile"
          }}
          steps {
            sh 'echo Test'
          }
        }
        
        stage('Build') {
          steps { 
            sh "pwd"
            sh "ls -la" 
            sh "docker build --file=productpage/Dockerfile --tag "$registry":productpage-"$BUILD_NUMBER" ."
            sh "docker build --file=ratings/Dockerfile --tag "$registry":ratings-"$BUILD_NUMBER" ."
            sh "docker build --file=details/Dockerfile --tag "$registry":details-"$BUILD_NUMBER" ."
            sh "docker build --file=mysql/Dockerfile --tag "$registry":mysql-"$BUILD_NUMBER" ."
          } 
        }

        stage('Publish') {
            steps {
                sh 'echo Publish'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'echo Deploy'
            }
        }
    }
}

