pipeline {

agent any

environment {

DOCKER_USER="sonali10"

}

stages {

stage('Clone Repo'){

steps{

git branch: 'main', url: 'https://github.com/SonaliMB/DevOpsDemo.git'

}

}

stage('Build Backend'){

steps{

sh 'docker build -t $DOCKER_USER/backend:latest ./backend'

}

}

stage('Build Frontend'){

steps{

sh 'docker build -t $DOCKER_USER/frontend:latest ./frontend'

}

}

stage('Docker Login'){

steps{

withCredentials([usernamePassword(credentialsId:'dockerhub',usernameVariable:'USER',passwordVariable:'PASS')]){

sh 'echo $PASS | docker login -u $USER --password-stdin'

}

}

}

stage('Push Images'){

steps{

sh 'docker push $DOCKER_USER/backend:latest'

sh 'docker push $DOCKER_USER/frontend:latest'

}

}

stage('Deploy to Kubernetes'){

steps{

sh 'kubectl apply -f k8s/'

}

}

stage('Verify'){

steps{

sh 'kubectl get pods'

}

}

}

}
