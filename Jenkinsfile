pipeline {
    agent any
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    
    stages {
        stage('Test') {
            agent { 
              docker {
                 image 'python:3.7.4-slim' 
            } }
            steps {
                withEnv(["HOME=${env.WORKSPACE}"]) { 
                  sh 'pip install --user -r productpage/requirements.txt --no-cache-dir' 
                  sh 'pip install --user -r productpage/test-requirements.txt --no-cache-dir'
                  sh 'python -m unittest discover productpage/tests/unit'
            }} 
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
