pipeline {
  agent any
  stages {
    stage('Build and push docker image') {
      steps {
        script {
          withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
            sh 'docker login -u ckr123 -p ${dockerhubpwd}'
          }
          sh 'docker build -t ckr123/food-menu-website:dev1 .'
          sh 'docker push ckr123/food-menu-website:dev1'
        }
      }
    }
    stage('deploy to another instance') {
      steps {
        sshagent(['testvm']) {
          sh "ssh ec2-user@172.31.32.84 docker run -d -p 8080:80 ckr123/food-menu-website:dev1"
        }
      }
    }
  }
}
