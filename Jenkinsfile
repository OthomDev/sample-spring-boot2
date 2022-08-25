pipeline {
    agent any
    environment {
        registry = "othom/springboot-app-gradle"
        registrycredential = 'dockerhub'
        dockerimage = ''
    }
    stages {
        stage('Git') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/OthomDev/sample-spring-boot2.git'
            }
        }
       
        stage('K8S Deploy') {
        steps{   
            script {
                withKubeConfig([credentialsId: 'EKS', serverUrl: '']) {
                    sh 'kubectl get node'
                    }
                }
            }
        }
        
       
        
    }
    
}
