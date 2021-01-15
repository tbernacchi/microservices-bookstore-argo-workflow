pipeline {
    agent any
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    
    stages {
        
        stage('Test') {
          steps {
            sh 'pwd' 
            sh "cd ~jenkins/workspace/infra-dev/reviews/ && /opt/gradle/gradle-4.8.1/bin/gradle clean build && cd .."
            sh 'docker-compose up -d'
            sh 'sleep 40' 
            sh 'docker exec -u root productpage curl --silent -X GET http://productpage:9080/health'
            sh 'docker exec -u root productpage curl --silent -X GET http://ratings:9080/health'
            sh 'docker exec -u root productpage curl --silent -X GET http://details:9080/health'
            sh 'docker exec -u root productpage curl -s -o /dev/null -w %{http_code} http://reviews:9080/health'
            sh 'docker exec -u root productpage python -m unittest discover tests/unit'
            sh 'sleep 10' 
          }
        }
        
        stage('Build') {
          steps { 
            sh "docker build --file=productpage/Dockerfile --tag $registry:productpage-$BUILD_NUMBER ."
            sh "docker build --file=ratings/Dockerfile --tag $registry:ratings-$BUILD_NUMBER ."
            sh "docker build --file=details/Dockerfile --tag $registry:details-$BUILD_NUMBER ."
            sh "docker build --file=mysql/Dockerfile --tag $registry:mysql-$BUILD_NUMBER mysql"
            sh "cd ~jenkins/workspace/infra-dev/reviews/ && /opt/gradle/gradle-4.8.1/bin/gradle clean build && cd .."
            sh "docker build --file=reviews/reviews-wlpcfg/Dockerfile --tag $registry:reviews-$BUILD_NUMBER reviews/reviews-wlpcfg"
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

