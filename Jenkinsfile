pipeline {
  agent { label 'jenkins-slave-pod' }
  stages {
    stage('prepare') {
      steps {
        sh 'echo test'
      }
    }
    stage('building docker image') {
      steps {
        container ('jenkins-slave-dind') {
          script {
            docker.build registry + ":$BUILD_NUMBER"
          }
        }
      }
    }
    stage('push docker image to dockerhub') {
      steps {
        container ('jenkins-slave-dind') {
            script {
              docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
            }
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
