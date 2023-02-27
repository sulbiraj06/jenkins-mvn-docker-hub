pipeline {
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sulbiraj06/jenkins-mvn-docker-hub.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sulbiraj/jenkins-mvn-docker-hub .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u sulbiraj -p ${dockerhubpwd}'

}
                   sh 'docker push sulbiraj/jenkins-mvn-docker-hub'
                }
            }
        }
        //stage('Deploy to k8s'){
            //steps{
                //script{
                    //kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
                //}
            //}
        //}
    }
}
