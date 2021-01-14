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
            sh "docker build --file=productpage/Dockerfile --tag $registry:productpage-$BUILD_NUMBER ."
            sh "docker build --file=ratings/Dockerfile --tag $registry:ratings-$BUILD_NUMBER ."
            sh "docker build --file=details/Dockerfile --tag $registry:details-$BUILD_NUMBER ."
            sh "docker build --file=mysql/Dockerfile --tag $registry:mysql-$BUILD_NUMBER mysql"
            sh "docker build --file=reviews/reviews-wlpcfg/Dockerfile --tag $registry:reviews-$BUILD_NUMBER reviews/reviews-wlpcfg"
            "sh "cd ~jenkins/workspace/infra-dev/reviews/ && /opt/gradle/gradle-4.8.1/bin/gradle -u gradle clean build && cd .."
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

