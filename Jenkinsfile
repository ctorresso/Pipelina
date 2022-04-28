pipeline {
  environment {
    imagename = "pdesar/nodejsapp"
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/ctorresso/Pipeline.git', branch: 'main', credentialsId: 'ctorresso-github-user-token'])

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("prueba")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:prueba"
         sh "docker rmi $imagename:latest"

      }
    }
  }
}
