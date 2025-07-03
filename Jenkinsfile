pipeline {
    agent any
    tools{
        maven 'maven 3.9.9'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Nhivas/devops-jenkins.git']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t nhivas27/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'efgh', variable: 'abcd')]) {
                   bat 'docker login -u nhivas27 -p <your password>'

}
                   bat 'docker push nhivas27/devops-integration'
                }
            }
        }
    }
}
