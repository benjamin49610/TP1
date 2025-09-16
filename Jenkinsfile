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
                    def latestTag = "benjamin49610/mywebsite:latest"
                    sh "docker build -t ${imageName} -t ${latestTag} ."
                }
            }
        }
        stage('Push the Docker Image to DockerHUb') {
              steps {
                script {
                
                    def imageName = "benjamin49610/mywebsite:${env.BUILD_NUMBER}"
                    def latestTag = "benjamin49610/mywebsite:latest"
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {

                    sh """
                    docker login -u benjamin49610 -p ${docker_hub}
                    docker push benjamin49610/mywebsite:${env.BUILD_NUMBER}
                    docker push ${latestTag}"""
                }
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

