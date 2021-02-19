pipeline {

  environment {
    registry = "anandsukan007/k8s-helloworld"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'github_cred', url: 'https://github.com/anandsukan007/kubernetes-helloworld.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'DOCKER_HUB_PASSWORD')]) {
              sh "docker login -u anandsukan007 -p ${DOCKER_HUB_PASSWORD}"
        }
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        sh " kubectl apply -f myweb.yaml "
      }
    }

  }

}
