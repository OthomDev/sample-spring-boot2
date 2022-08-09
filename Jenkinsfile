pipeline {
    agent any
    stages {
        stage('Git') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/OthomDev/sample-spring-boot.git'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew check'
            }
        }
        
    }
    
    post {
            always {
                archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
                junit 'build/reports/**/*.xml'
            }
   }
}
