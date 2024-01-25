pipeline {
    agent any
    tools{
        maven '3.8.5'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/myusecase2023/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    bat 'docker build -t mydockerhub111/devops-integration .'
                }
            }
        }
        stage('Push Image to DockerHub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'mydockerhub', variable: 'dockerhubpwd')]) {
					bat 'docker login -u mydockerhub111 -p persist123'
				   }
                   bat 'docker push mydockerhub111/devops-integration'
                }
            }
        }
    }

}