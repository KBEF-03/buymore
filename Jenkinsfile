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
    }
}
        