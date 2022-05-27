pipeline {
    environment {
        registry = "rizwan141/riz244"
        registryCredential = 'dockerhub'
    }
    agent any
    stages {
        stage('Checkout') {
            steps {
                     // Get code from a GitHub repository
                    git url:'', branch: 'main',
                    credentialsId: 'github'
            }
        }
        stage('Building image') {
            steps{
                sh 'docker build -t jenkintest:latest .'
                  sh 'docker tag jenkintest s/jenkintest:latest'
                sh 'docker tag jenkintest s/jenkintest:$BUILD_NUMBER'
            }
        }
        stage('Deploy our image') {
            steps {
                withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
              sh  'docker push s/jenkintest:latest'
              sh  'docker push s/jenkintest:$BUILD_NUMBER'
                }
            }
        }
    }
}
