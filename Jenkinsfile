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
            sh "docker build --file=productpage/Dockerfile --tag "$registry":"$BUILD_NUMBER" ."
            sh "docker build --file=ratings/Dockerfile --tag "$registry":"$BUILD_NUMBER" ."
            sh "docker build --file=details/Dockerfile --tag "$registry":"$BUILD_NUMBER" ."
            sh "docker build --file=mysql/Dockerfile --tag "$registry":"$BUILD_NUMBER" ."
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

