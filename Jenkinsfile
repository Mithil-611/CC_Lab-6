pipeline {
 agent any

 stages {

  stage('Build Backend Image') {
   steps {
    sh 'docker build -t backend-app CC_LAB-6/backend'
   }
  }

  stage('Deploy Backends') {
   steps {
    sh '''
    docker rm -f backend1 backend2 nginx-lb || true
    docker network rm lab6-network || true
    docker network create lab6-network

    docker run -d --name backend1 --network lab6-network backend-app
    docker run -d --name backend2 --network lab6-network backend-app

    docker build -t nginx-lb CC_LAB-6/nginx

    docker run -d --name nginx-lb -p 80:80 \
    --network lab6-network nginx-lb
    '''
   }
  }

 }
}
