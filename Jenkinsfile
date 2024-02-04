pipeline {
   agent any

       
    stages{   
        stage('Cleanup Workspace') {
            steps {
                script {
                    deleteDir()
                }
            }
        }


       stage('checkout from git repo') {
               steps {
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Aniediogo/buymore.git']])
               }
       }


       stage('Check repo for secrets') {
                steps {
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

       
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'docker-id', variable: 'cred')]) {
                   sh 'docker login -u aniediogo -p ${cred}'

}
                   sh 'docker push aniediogo/buymore:1.1'
                }
            }
        }


    }
}
