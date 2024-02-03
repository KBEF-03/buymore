pipeline {
   agent any

   stages {
       stage('checkout from git repo') {
               steps {
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Aniediogo/buymore.git']])
               }
       }



        stage('Check repo for secrets') {
               steps {
                 sh 'rm -rf trufflehog-result.json || true'
                 sh 'docker run gesellix/trufflehog --json https://github.com/Aniediogo/buymore.git > trufflehog-result.json'
               }
           }   
       

       stage('Build docker image') {
            steps {
                script {
                    sh 'docker rmi buymore:1'  
                    sh 'docker build -t buymore:1 .'
                }
            }
        }
   }
}   
