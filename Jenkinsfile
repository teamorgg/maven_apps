pipeline {
    agent any 
    stages {
        stage('Code Checkout') { 
            steps {
                sh 'echo code checkout'
                git credentialsId: 'github-sonar', url: 'https://github.com/itrainnikhil/maven_apps.git'
            }
        }
        stage('Build') { 
            steps {
              withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.0') {
               sh 'mvn clean compile'
             } 
            }
        }
        stage('Test') { 
            steps {
               withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.0') {
               sh 'mvn test'
             }  
            }
        }
        
        stage('code analysis') { 
            steps {
                withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.0') {
                sh 'mvn sonar:sonar \
                    -Dsonar.projectKey=maven-nikhil \
                    -Dsonar.organization=itrainnikhil \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=52e9e505fcec884b91de3535c078f1dcbc552b95'
             }  
            }
        }
        stage('Package') { 
            steps {
                withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.0') {
               sh 'mvn package'
             }  
            }
        }
       
    }
}
