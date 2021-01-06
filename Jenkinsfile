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
                sh 'echo $HOME'
            }
        }
    }
    
    agent {
      dockerfile { 
      filename "details/Dockerfile"
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
