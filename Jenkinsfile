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
            sh '''#!/bin/bash
              "docker build --file=productpage/Dockerfile" --tag registry + ":$BUILD_NUMBER" ."
              "docker build --file=ratings/Dockerfile --tag registry + ":$BUILD_NUMBER" ." 
              "docker build --file=details/Dockerfile --tag registry + ":$BUILD_NUMBER" ."
              "docker build --file=mysql/Dockerfile --tag registry + ":$BUILD_NUMBER" ."
              '''
          } 
        }

        stage('Publish') {
            steps {
                sh 'echo olaa publish'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'echo olaaa'
                sh 'echo Aqui tenho que fazer um kubectl get health sei la'
            }
        }
    }
}

