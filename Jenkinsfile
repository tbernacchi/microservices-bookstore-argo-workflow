pipeline {
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    agent { dockerfile true }
    stages {
        stage('Build') {
            steps {
                sh 'node --version'
                sh 'svn --version'
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

