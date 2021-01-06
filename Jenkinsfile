pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    agent { 
      dockerfile { 
      filename "productpage/Dockerfile"
      }
    } 
    stages {
        stage('Build') {
            steps {
                sh 'curl -m 5 -o /dev/null -s -w "%{http_code}\n" http://127.0.0.1:9080/health'
            }
        }
    }
} 
