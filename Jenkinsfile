pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    agent { 
      dockerfile { 
      filename "frontend/Dockerfile"
      }
    } 
    stages {
        stage('Build') {
            steps {
                sh 'echo $HOME'
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

