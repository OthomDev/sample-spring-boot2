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
        stage('build'){
            steps{   
                  sh 'mvn -B -DskipTests clean package'
                
            }
       }
        stage('check env'){
            steps{
                sh "mvn -v"
                sh "java -version"
            }
        }
        
    }
    
}
