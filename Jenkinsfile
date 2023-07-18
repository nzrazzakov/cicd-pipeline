pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh 'script scripts/test.sh'
      }
    }

    stage('Docker Image Build') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

    stage('Docker Image Push') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_creds')
          {
            dockerImage.push()
          }
        }

      }
    }

  }
  environment {
    registry = 'nzrazzakov/cicdjenkins'
    registryCredential = 'dockerhub_creds'
    dockerImage = ''
  }
}