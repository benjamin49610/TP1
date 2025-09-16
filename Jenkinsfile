pipeline {
    agent any

    stages {
        stage('Hello World') {
            steps {
                echo 'Bonjour Samir ! Je teste mon pipeline'
            }
        }
        stage('Build Docker Image') {
              steps {
              sh 'docker build -t benjamin49610/myfirstdocker .'
            }
        }
        stage('Push the Docker Image to DockerHUb') {
              steps {
                script {
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {
                    sh 'docker login -u benjamin49610 -p ${docker_hub}'
                                                             }
                    sh 'docker push benjamin49610/myfirstdocker'
                }
            }
        }
        stage('Check PATH') {
        steps {
            sh 'echo $PATH'
        }
        } 
        stage('Deployement on Kube') {
             steps {
                script {
                        withKubeConfig([credentialsId: 'minikubeID', caCertificate: '/var/lib/jenkins/kube_ca.cert',  serverUrl: 'https://192.168.49.2:8443']) {
                            sh 'minikube kubectl -- apply -f deployement.yaml'
                            sh 'minikube kubectl -- get pods'
                        }
                    }
                }
            }
    }
}


