pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/OthomDev/sample-spring-boot.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mkdir lib'
                sh 'cd lib/ ; wget https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.7.0/junit-platform-console-standalone-1.7.0-all.jar'
                sh 'cd src/main/java/com/example/springboot ; javac -cp "../lib/junit-platform-console-standalone-1.7.0-all.jar" Application.java HelloController.java'
            }
        }
          stage('Test'){
            steps{
                sh 'cd src/test/java/com/example/springboot ; java -jar ../lib/junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class HelloControllerIT.java'
                sh 'cd src/test/java/com/example/springboot ; java -jar ../lib/junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class HelloControllerTest.java'
            }
        }
        
    }
}
