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
              sh 'docker build -t MyFirstDocker .'
            }
        }
    }
}
