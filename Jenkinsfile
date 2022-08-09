pipeline {
    agent any
    stages {
        stage('Git') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/OthomDev/sample-spring-boot.git'
            }
        }
        stage('build'){
            withMaven(maven: 'mvn') {
                sh "mvn clean package"
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
