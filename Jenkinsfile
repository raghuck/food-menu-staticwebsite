pipeline {
  agent any
  stages {
    stage('Build and push docker image') {
      steps {
        script {
          withCredentials([string(credentialsId: 'savitha2789', variable: 'docker')]) {
            sh 'docker login -u savitha2789 -p ${docker}'
          }
          sh 'docker build -t ckr123/food-menu-website:dev1 .'
          sh 'docker push ckr123/food-menu-website:dev1'
        }
      }
    }
    stage('deploy to another instance image') {
      steps {
        sshagent(['8d329f24-9425-4d71-9188-af4c04d7feda']) {
        }
        script {
          sh "ssh ec2-user@172.31.32.84 'docker run -d -p 8080:8080 ckr123/food-menu-website:dev1'"
        }
      }
    }
  }
}
