pipeline {
    agent {label "ubuntu"}
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-sharan')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/kandulasharan/Node.js.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t kandulasharankumar/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push kandulasharankumar/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

