pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    agent { 
      dockerfile { 
      filename "details/Dockerfile"
      filename "productpage/Dockerfile"
      }
    } 
    
    stages {
        stage('Build') {
            steps {
                sh 'echo $HOME'
            }
        }
    }
}
