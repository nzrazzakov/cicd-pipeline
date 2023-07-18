pipeline {
  agent any
  stages {
    stage('Build') {
      environment {
        DOCKERVERSION = '18.03.1-ce'
      }
      steps {
        sh '''curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKERVERSION}.tgz \\
  && tar xzvf docker-${DOCKERVERSION}.tgz --strip 1 \\
                 -C /usr/local/bin docker/docker \\
  && rm docker-${DOCKERVERSION}.tgz'''
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
        sh 'docker build -t nzrazzakov/jenkinscicd .'
      }
    }

  }
}