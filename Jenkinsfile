pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Git') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/OthomDev/sample-spring-boot.git'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn --version'
                sh 'mvn test'
            }
        }
       
        
    }
    
}
