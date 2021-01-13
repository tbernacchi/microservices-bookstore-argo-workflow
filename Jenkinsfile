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
                  sh 'docker build productpage/Dockerfile --tag registry + ":$BUILD_NUMBER"'
            }

            agent { 
              docker {
                 image 'websphere-liberty:19.0.0.6-javaee8' 
            } }
            steps {
                  sh 'cd reviews/'
                  sh 'docker run --rm -u root -v "$(pwd)":/home/gradle/project -w /home/gradle/project gradle:4.8.1 gradle clean build'
                  sh 'cd ..'
                  sh 'docker build reviews/reviews-wlpcfg/Dockerfile --tag registry + ":$BUILD_NUMBER"'
            }
            
            agent { 
              docker {
                 image 'node:12.9.0-slim' 
            } }
            steps {
                  sh 'docker build ratings/Dockerfile --tag registry + ":$BUILD_NUMBER"'
            }
            
            agent { 
              docker {
                 image 'ruby:2.7-rc-slim' 
            } }
            steps {
                  sh 'docker build details/Dockerfile --tag registry + ":$BUILD_NUMBER"'
            }
            
            agent { 
              docker {
                 image 'mysql:8.0.17' 
            } }
            steps {
                  sh 'docker build mysql/Dockerfile --tag registry + ":$BUILD_NUMBER"'
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
