pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    agent { 
      dockerfile { 
      filename "productpage/Dockerfile"
      filename "reviews/reviews-wlpcfg/Dockerfile"
      filename "details/Dockerfile"
      filename "ratings/Dockerfile"
      }
    } 
    
    stages {
        stage('Build') {
            steps {
                sh 'env'
            }
        }
    }
}
