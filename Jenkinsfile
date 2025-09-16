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
                script {
                    def imageName = "benjamin49610/mywebsite:${env.BUILD_NUMBER}"
                    sh "docker build -t ${imageName} ."
                }
            }
        }
        stage('Push the Docker Image to DockerHUb') {
              steps {
                script {
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {
                    sh "docker login -u benjamin49610 -p ${docker_hub}"
                                                             }
                    sh "docker push ${imageName}"
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
                        withKubeConfig([credentialsId: 'minikubeID', serverUrl: 'https://192.168.49.2:8443']) {
                            sh 'minikube kubectl -- apply -f deployement.yaml'
                            sh 'minikube kubectl -- get pods'
                        }
                    }
                }
            }
    }
}

