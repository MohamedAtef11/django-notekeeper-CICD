pipeline {
    agent any

    stages {
        stage("Docker login"){
            steps{
                    withCredentials([string(credentialsId: 'DockerHubPwd', variable: 'DockerHubPwd')]) {
                    sh "docker login -u muhammadatef -p ${DockerHubPwd}"
                    
                }
            }
        }
        stage('Build and push images ') {
            steps {
                
                sh " docker build -t muhammadatef/django-notekeeper:latest -f ./django-notekeeper/Dockerfile . "
                sh " docker push muhammadatef/django-notekeeper:latest" 
                    
            }
        }

    }
}

node {
  stage('List pods') {
    withKubeConfig([credentialsId: 'kube-config']) {
        sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
        sh 'chmod u+x ./kubectl'  
       
        sh './kubectl apply -f ./Kubernetes_files/'
        sh './kubectl get pods'
    }
  }
}



