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
                    sh './mvnw clean compile'
                
            }
       }
        stage('Test') {
            steps {
                sh './mvnw test'
                // bat '.\\mvnw test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        
    }
    
}
