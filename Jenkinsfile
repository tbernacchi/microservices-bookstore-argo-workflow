pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    agent { 
      dockerfile { 
      filename "details/Dockerfile"
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
