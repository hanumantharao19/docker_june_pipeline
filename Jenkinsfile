pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    
    stages {
        
        stage('git checkout') {
            
            steps{
                git credentialsId: 'GitHubID', url: 'https://github.com/hanumantharao19/docker-pipeline-mhr.git'
            }
        }
        
        stage('maven build') {
            
            steps{
                sh 'mvn clean install'
            }
        }
        
        stage('docker build') {
            steps {
                sh 'docker build -t hanumantharao1986/julyjavadockerimage:v2 .'
            }
        }
        
        stage('docker login ') {
            
            steps{
                script {
                     withCredentials([string(credentialsId: 'dockerhubjune', variable: 'dockerhubjune')]) {
                     sh 'docker login -u hanumantharao1986 -p ${dockerhubjune}'
                   }
               }
            }
        }
        
        stage('deploy image to docker registry') {
            
            steps {
                sh 'docker push hanumantharao1986/julyjavadockerimage:v2'
            }
        }
        
        
    }
}
