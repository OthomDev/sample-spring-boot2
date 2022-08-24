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
        /*stage('sonarqube') {
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
        
        stage('Quality gate') {
           steps {
                script {
                      timeout(time: 5, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                       }
                 }
           }
         }*/
        stage('Build Image') {
            steps {
                script {
                    // reference: https://www.jenkins.io/doc/book/pipeline/jenkinsfile/
                    img = registry + ":${env.BUILD_ID}"
                    // reference: https://docs.cloudbees.com/docs/admin-resources/latest/plugins/docker-workflow
                    dockerImage = docker.build("${img}")
                }
            }
        }
        stage('Push To DockerHub') {
            steps {
                script {
                    docker.withRegistry( 'https://registry.hub.docker.com ', registryCredential ) {
                        // push image to registry
                        dockerImage.push()
                    }
                }
            }
        }
        stage('K8S Deploy') {
        steps{   
            script {
                withKubeConfig([credentialsId: 'K8S', serverUrl: '']) {
                    sh ('kubectl apply -f  eks-deploy-k8s.yaml')
                    }
                }
            }
        }
        
       
        
    }
    
}
