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


       

       stage('checkout from git repo') {
               steps {
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Aniediogo/buymore.git']])
               }
       }

     
       stage('Check for secret in repo'){
         steps{
            sh 'docker run gesellix/trufflehog --json https://github.com/Aniediogo/buymore.git > trufflehog-result.json'
         }
       }


       stage('SCA test with snyk'){
         steps{
            echo 'snyk testing .........'
            snykSecurity(
               snykInstallation: 'snyk',
               snykTokenId: 'snyk',
            )
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