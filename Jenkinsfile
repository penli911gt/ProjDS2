pipeline {
    agent any

    tools {
        maven 'Maven3'  // correspond au nom que tu as donné dans l'interface Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/penli911gt/ProjDS2.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv('sonar-token') { // à adapter selon ton config
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-app .'
            }
        }
    }
}
