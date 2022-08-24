pipeline {
    agent any
    environment {
        registry = "othom/springboot-app-gradle"
        registrycredential = 'dockerhub'
        dockerimage = ''
        AWS_CREDENTIALS = credentials('K8S')
        EKS_CLUSTER_NAME = "demo-eks"
        EKS_CLUSTER_REGION = "us-east-2"
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
            sh """
                    aws eks update-kubeconfig --region ${EKS_CLUSTER_REGION} --name ${EKS_CLUSTER_NAME}
                    kubectl cluster-info
                """

            }
        }
        
       
        
    }
    
}
