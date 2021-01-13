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
            sh 'echo testing'
          }
        }
        
        stage('Build') {
          steps { 
            sh '''#!/bin/bash
              docker build productpage/Dockerfile --tag registry + ":$BUILD_NUMBER"
              cd reviews/
              docker run --rm -u root -v "$(pwd)":/home/gradle/project -w /home/gradle/project gradle:4.8.1 gradle clean build
              cd ..
              docker build reviews/reviews-wlpcfg/Dockerfile --tag registry + ":$BUILD_NUMBER"
              docker build ratings/Dockerfile --tag registry + ":$BUILD_NUMBER"
              docker build details/Dockerfile --tag registry + ":$BUILD_NUMBER"
              docker build mysql/Dockerfile --tag registry + ":$BUILD_NUMBER"
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

