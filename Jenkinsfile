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
        stage('Deployement on Kube') {
             steps {
                script {
                    // Charger le fichier kubeconfig en toute sécurité
                    withCredentials([file(credentialsId: 'minikubeID', variable: 'KUBECONFIG')]) {
                        withKubeConfig([credentialsId: 'minikubeID']) {
                            sh 'kubectl apply -f deployment.yaml'
                            sh 'kubectl get pods'
                        }
                    }
                }
            }
    }
}
}

