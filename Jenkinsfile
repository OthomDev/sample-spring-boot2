pipeline {
    agent any
    environment {
        registry = "othom/springboot-app-gradle"
        registrycredential = 'dockerhub'
        dockerimage = ''
        AWS_CREDENTIALS = credentials('EKS') 
        EKS_CLUSTER_NAME = "demo-eks"
        EKS_CLUSTER_REGION = "us-east-1"
    }
    stages {
        stage('Git') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/OthomDev/sample-spring-boot2.git'
            }
        }
       
        stage('Deploy App') {
            steps {
                sh """
                    aws eks update-kubeconfig --region ${EKS_CLUSTER_REGION} --name ${EKS_CLUSTER_NAME}
                    kubectl cluster-info dump
                """            
            }
   }
        
       
        
    }
    
}
