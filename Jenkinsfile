pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/penli911gt/ProjDS2.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'  // Change package to install
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-token') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Docker Build') {  // ADD this stage
            steps {
                sh 'docker build -t springboot-app .'
            }
        }
    }
}
