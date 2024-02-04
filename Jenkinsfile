pipeline {
   agent any

   environment{
      APP_NAME = 'buymore'
      RELEASE = '1.0.1'
      DOCKER_USER = 'aniediogo'
      DOCKER_PASS = 'dockerhub'
      IMAGE_NAME = '${DOCKER_USER}' + '/' + '${APP_NAME}'
      IMAGE_TAG = '${RELEASE}-${BUILD_NUMBER}'
   }
       
    stages{   
       stage('checkout from git repo') {
               steps {
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Aniediogo/buymore.git']])
               }
       }


        stage('Check repo for secrets') {
               steps {
                 sh 'rm -rf trufflehog-result.json || true'
                 sh 'docker run gesellix/trufflehog --json https://github.com/Aniediogo/buymore.git > trufflehog-result.json'
                 sh 'cat trufflehog-result.json'
               }
           }   

        stage('build and push docker image to docker hub'){
               steps{
                  script{
                      docker.withRegistry('',DOCKER_PASS){
                        docker_image = docker.build = '${IMAGE_NAME}'
                      }

                      docker.withRegistry('',DOCKER_PASS){
                        docker_image.push('${IMAGE_TAG}')
                        docker_image.push('latest')
                      }
              }
            }
              
        }
    } 
} 

        