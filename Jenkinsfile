pipeline {
    environment {
        registry = "siva997/siva44"
        registryCredential = 'dockerhub'
    }
    agent any
    stages {
        stage('Checkout') {
            steps {
                     // Get code from a GitHub repository
                    git url:'https://github.com/Sivaram122/sample.git', branch: 'main',
                    credentialsId: 'github'
            }
        }
        stage('Building image') {
            steps{
                sh 'docker build -t jenkintest:latest .'
                  sh 'docker tag jenkintest siva997/jenkintest:latest'
                sh 'docker tag jenkintest siva997/jenkintest:$BUILD_NUMBER'
            }
        }
        stage('Deploy our image') {
            steps {
                withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
              sh  'docker push siva997/jenkintest:latest'
              sh  'docker push siva997/jenkintest:$BUILD_NUMBER'
                }
            }
        }
    }
}
