pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    agent { 
      dockerfile { 
      filename "reviews/reviews-wlpcfg/Dockerfile"
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
