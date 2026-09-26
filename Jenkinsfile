pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat '''
                    mvn org.sonarsource.scanner.maven:sonar-maven-plugin:5.8.0.7211:sonar ^
                    -Dsonar.projectKey=sast-demo ^
                    -Dsonar.projectName=SAST-Demo
                    '''
                }
            }
        }
    }
}