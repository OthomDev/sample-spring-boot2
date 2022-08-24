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
                withKubeConfig([credentialsId: 'K8S', serverUrl: '']) {
                    sh ('sudo kubectl apply -f  eks-deploy-k8s.yaml')
                    }
                }
            }
        }
        
       
        
    }
    
}
