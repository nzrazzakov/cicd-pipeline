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
        sh 'scripts script/test.sh'
      }
    }

    stage('Docker Image Build') {
      steps {
        sh 'docker build -t nzrazzakov/jenkinscicd'
      }
    }

  }
}