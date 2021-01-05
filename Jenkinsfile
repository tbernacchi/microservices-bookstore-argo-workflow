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
                sh 'cd productpage'
            }
        }
    
    stage('Publish') {
      environment {
        registryCredential = 'dockerhub'
      }
      steps{
        script {
            def appimage = docker.build registry + ":$BUILD_NUMBER"
            docker.withRegistry( '', registryCredential ) {
                appimage.push()
                appimage.push('latest')
            }
          }
      }
    }
  }
}

