pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t abderhmanemahdigharzouli/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerpwd')]) {
              sh 'docker login -u abderhmanemahdigharzouli -p ${dockerpwd}'
}
              sh 'docker push abderhmanemahdigharzouli/devops-integration:latest'
                }
            }
        }
    
      
    }
}