pipeline {
    agent {

    dockerfile true 

    environment {
        registry = "tadeuuuuu/infra-developer"
        #GOCACHE = "/tmp"
    }
    stages {
        stage('Build') {
              
        }

    agent {
    // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
    dockerfile {
        filename './productpage/Dockerfile'
        dir 'build'
        label 'my-defined-label'
        additionalBuildArgs  '--build-arg version=1.0.0'
        args '-v /tmp:/tmp'
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
