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

