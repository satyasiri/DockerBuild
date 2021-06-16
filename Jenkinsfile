pipeline {
  environment {
    registry = "dopjh/project1java"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }

  agent any

  stages {


    stage('Building Image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Deploying Image') {
      steps {
        script {
          docker.withRegistry( '', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Cleaning up') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
