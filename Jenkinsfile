pipeline {
    agent any
    environment {
        registry = "othom/springboot-app"
        registrycredential = 'dockerhub'
        dockerimage = ''
    }
    tools {
        maven 'Maven'
         gradle "Gradle"
    }
    stages {
        stage('Git') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/OthomDev/sample-spring-boot.git'
            }
        }
        stage('Build') {
            steps {
                sh 'java -version'
                sh "chmod +x gradlew"
                sh './gradlew assemble'
            }
          }
        stage('Test') {
            steps {
                sh 'java -version'
                sh "chmod +x gradlew"
                sh './gradlew test'
            }
        }
        stage('Publish Test Coverage Report') {
         steps {
           step([$class: 'JacocoPublisher',
                execPattern: '**/build/jacoco/*.exec',
                classPattern: '**/build/classes',
                sourcePattern: 'src/main/java',
                exclusionPattern: 'src/test*'
                ])
            }
        }
        stage('SonarCloud analysis') {
            steps{
                script{
                    def scannerHome = tool 'scanner';
                      withSonarQubeEnv('SonarCloud') {
                           sh './gradlew sonarqube'
                      }
                }
            }
        
        }
        stage('Quality gate') {
           steps {
                script {
                      timeout(time: 5, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                       }
                 }
           }
         }
       
        
    }
    
}
