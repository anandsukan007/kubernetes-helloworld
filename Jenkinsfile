pipeline {

  environment {
    registry = "anandsukan007/k8s-helloworld"
   // dockerImage = ""
    Imagetagname = "6.0.0"
  }

  agent { label 'kubemaster' }

  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'github_cred', url: 'https://github.com/anandsukan007/kubernetes-helloworld.git'
      }
    }

    stage('Build Docker Image'){
            //agent { label 'slave_kubemaster' }
        steps{
          sh 'docker build -t anandsukan007/k8s-helloworld:${Imagetagname} .'
    }
    }
    
    stage('Push Docker Image'){
    steps{
        withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'DOCKER_HUB_PASSWORD')]) {
              sh "docker login -u anandsukan007 -p ${DOCKER_HUB_PASSWORD}"
        }
        sh "docker push anandsukan007/k8s-helloworld:${Imagetagname} "
     }
     }
        stage('Deploy to K8s'){
            steps{
        sh " pwd "  
        sh " hostname "
        sh " ls -ltr "
       // sh " cp -R myweb/* . "      
        sh " /usr/local/bin/helm upgrade --install myweb . "  
    }
    }
     }
     }
