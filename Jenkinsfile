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


       
       stage('build docker image') {
              steps{
                  script{
                     sh 'docker build -t aniediogo/buymore:1.1 .'
                }
            }
       }
   
       
       stage('trivy scan') {
              steps{
                     sh 'trivy image aniediogo/buymore:1.1'
                }
            }

   
//        stage('push docker to docker hub'){
//          steps{
//             script{
//                       withCredentials([string(credentialsId: 'dockerbub', variable: 'cred')]) {
//                       sh 'docker login -u aniediogo -p ${cred}'

// }
//                       sh 'docker push aniediogo/buymore:1.1'
//             }
//          }
  
//        }

       
    }
}    