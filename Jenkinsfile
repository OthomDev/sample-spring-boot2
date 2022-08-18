pipeline {
    agent any
    environment {
        registry = "othom/springboot-app"
        registrycredential = 'dockerhub'
        dockerimage = ''
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
        stage('sonarqube') {
            agent {
                docker { image 'sonarsource/sonar-scanner-cli' } 
            }
            steps {
                sh 'echo scanning!'
                
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
