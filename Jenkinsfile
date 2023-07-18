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
        sh 'docker build -t nzrazzakov/jenkinscicd .'
      }
    }

    stage('Docker Image Push') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_creds') {image.push("${env.BUILD_NUMBER}")
          image.push("latest")}
        }

      }
    }

  }
}