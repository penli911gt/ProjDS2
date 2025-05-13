pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQubeServer' // Nom défini dans Jenkins > Manage Jenkins > Configure SonarQube
        IMAGE_NAME = 'springboot-app' // Nom Docker que tu veux
    }

    stages {
        stage('Cloner le projet GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/penli911gt/ProjDS2.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=springboot-project -Dsonar.host.url=http://localhost:9000'
                }
            }
        }

        stage('Attente du Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline terminé avec succès."
        }
        failure {
            echo "❌ Le pipeline a échoué."
        }
    }
}
