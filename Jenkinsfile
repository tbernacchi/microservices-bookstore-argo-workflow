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
            sh 'sleep 20'
            sh 'docker exec -u root productpage curl -s -o /dev/null -w %{http_code} http://reviews:9080/health'
            sh 'docker exec -u root productpage pip install -r test-requirements.txt'
            sh 'sleep 20' 
            sh 'docker exec -u root productpage python -m unittest discover tests/unit'
          }
        }
        
        stage('Build') {
          steps { 
            sh 'ls -la productpage/'
            sh "docker build --file=productpage/Dockerfile --tag $registry:productpage-$BUILD_NUMBER ."
            sh "docker build --file=ratings/Dockerfile --tag $registry:ratings-$BUILD_NUMBER ."
            sh "docker build --file=details/Dockerfile --tag $registry:details-$BUILD_NUMBER ."
            sh "docker build --file=mysql/Dockerfile --tag $registry:mysql-$BUILD_NUMBER mysql"
            sh "cd ~jenkins/workspace/infra-dev/reviews/ && /opt/gradle/gradle-4.8.1/bin/gradle clean build && cd .."
            sh "docker build --file=reviews/reviews-wlpcfg/Dockerfile --tag $registry:reviews-$BUILD_NUMBER reviews/reviews-wlpcfg"
          } 
        }

        stage('Publish') {
          environment {
            registryCredential = 'dockerhub'
          }
          steps {
                script { 
                  docker.withRegistry( '', registryCredential ) {  
                    sh '''for i in `echo productpage ratings details mysql reviews`;do 
                            docker push $registry:$i-$BUILD_NUMBER;
                          done
                        '''
                  }
                }
          } 
        }
        
        stage('Deploy to Production') {
            steps {
              script { 
                image-productpage = "$registry:productpage-$BUILD_NUMBER"
                image-details = "$registry:details-$BUILD_NUMBER"
                image-ratings = "$registry:ratings-$BUILD_NUMBER"
                image-mysql = "$registry:mysql-$BUILD_NUMBER"
                image-reviews = "$registry:reviews-$BUILD_NUMBER"
                  sh "ansible-playbook kubernetes/playbook.yml --extra-vars \"image-productpage=${image-productpage}\" --extra-vars \"image-details=${image-details}\" --extra-vars \"image-ratings=${image-ratings}\" --extra-vars \"image-mysql=${image-mysql}\" --extra-vars \"image-reviews=${image-reviews}\""
              } 
            }
            
            post {
                success {
                    echo "Successfully deployed to Production"
                }
                failure {
                    echo "Failed deploying to Production"
                }
            }
        }
    }
    post {
      always {
        sh "docker-compose down -v"
        }
    }
}

