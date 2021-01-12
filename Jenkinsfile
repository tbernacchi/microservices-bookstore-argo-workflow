pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    
    stages {
        stage('Test') {
            agent { 
              docker {
                 image 'python:3.7.4-slim' 
              }
            steps {
                  sh 'pip install -r productpage/test-requirements.txt'
                  sh 'python -m unittest discover tests/unit'
            }
        }
        
        stage('Build') {
            agent { 
              docker {
                 image 'python:3.7.4-slim' 
            }
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
    }  
} 
