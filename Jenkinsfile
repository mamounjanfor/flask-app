pipeline {
      agent any
          stages {
               stage('Clone Repository') {
               steps {
               checkout scm
               }
          }
          stage('Build Image') {
               steps {
               sh "docker build -t 19841022/flask ."
               }
         }
         stage('Push image') {
               steps {
               sh 'docker push 19841022/flask'
               }
         }
         stage('copy the files') {
               steps {
               sh "scp -o StrictHostKeyChecking=no deploy.yaml ubuntu@3.132.121.58:/home/ubuntu"
               sh "scp -o StrictHostKeyChecking=no ansi.yml ubuntu@3.132.121.58:/home/ubuntu"
               }
         }       
         stage('ansible deploy') {
               steps {
               sh 'ansible -m ping all'
               sh 'ansible-playbook ansi.yml'
               }
         stage('expose the app') {
               steps {
               sh 'ssh ubuntu@3.132.121.58'
               }
         }
         stage('Testing') {
              steps {
                    echo 'Testing...'
                    }
         }
    }
}
