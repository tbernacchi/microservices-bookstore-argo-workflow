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
            agent { 
              docker {
                 image 'python:3.7.4-slim' 
            } }
            steps {
                  sh 'echo olaaa build'
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
