pipeline {
  agent any
  stages {
    stage('Build') {
      environment {
        DOCKERVERSION = '18.03.1-ce'
      }
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh 'script scripts/test.sh'
      }
    }

    stage('Buld Docker Image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

    stage('Push') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()}
          }

          sh 'sh "docker rmi $registry:$BUILD_NUMBER"'
        }
      }

    }
    environment {
      registry = 'nzrazzakov/cicdjenkins'
      registryCredential = 'dckr_pat_llIGArmeP2riHvIK4VPOORse43I'
      dockerImage = ''
    }
  }