pipeline {
    agent any

    stages {
        stage('Checkout from Git Repo') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/KBEF-03/buymore.git']]
                ])
            }
        }

        stage('Build Docker Image') {
    steps {
        script {
            sh 'docker build -t buymore:1 .'
            echo 'Docker image built successfully!'
        }
    }
}

        