pipeline {
    agent {label "linux"}
    tools {
        maven 'maven'
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/lucas-lin-sonarsource/maven-basic.git' // Use your Git repository URL
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('SonarQube Analysis') {
            environment {
                SONAR_HOST_URL = 'https://lucas-lin-sq2025.ngrok.app' // Replace with your SonarQube URL
                SONAR_AUTH_TOKEN = credentials('d230cb3e-12a7-45d6-8420-f0839c9c7211') // Store your token in Jenkins credentials
            }
            steps {
                sh 'mvn sonar:sonar -Dsonar.projectKey=maven-basic -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_AUTH_TOKEN -X'
            }
        }
        
    }
}
