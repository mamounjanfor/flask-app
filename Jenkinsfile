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
         stage('ansible deploy') {
               steps {
               sh 'ansible-playbook ansib.yml'
               }
         }
         stage('copy deployment file') {
               steps {
               sh "scp -o StrictHostKeyChecking=no deploy.yaml ubuntu@3.145.195.158:/home/ubuntu"
               }
         }       
         stage('Deploy k8') {
               steps {
               sh 'ssh ubuntu@3.145.195.158 kubectl apply -f deploy.yaml'    
               }
         }
         stage('Testing') {
              steps {
                    echo 'Testing...'
                    }
         }
}
}
