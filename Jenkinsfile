pipeline {
    agent any
    environment {
        // Load SonarQube token securely
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                bat "mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.token=%SONAR_TOKEN%"
            }
        }
    }
}
