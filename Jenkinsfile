pipeline {
    agent any

    tools {
        sonarScanner 'SonarScanner'
    }

    stages {
        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat '''
                    sonar-scanner ^
                    -Dsonar.projectKey=simple-app ^
                    -Dsonar.sources=. ^
                    -Dsonar.login=YOUR_TOKEN
                    '''
                }
            }
        }

        stage('Run App') {
            steps {
                bat 'java -jar app.jar'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}