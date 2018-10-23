pipeline {
  agent any
  stages {
    stage('prepare') {
      steps {
        sh 'echo test'
      }
    }
    stage('building docker image') {
      steps {
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }
    stage('push docker image to dockerhub') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }

      }
    }
  }
  environment {
    registry = 'stefku/hello-world'
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
}