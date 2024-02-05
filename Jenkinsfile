pipeline {
   agent any

       
    stages{  
       stage('Clean up workspace'){
         steps{
            script{
               deleteDir()
            }
         }
       }


       stage('Check for secret in repo'){
         steps{
            sh 'docker run gesellix/trufflehog --json https://github.com/Aniediogo/buymore.git > trufflehog-result.json'
         }
       }

       stage('checkout from git repo') {
               steps {
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Aniediogo/buymore.git']])
               }
       }


       stage('build docker image') {
              steps{
                  script{
                     sh 'docker build -t buymore:1 .'
                }
            }
       }

       
    }
}    