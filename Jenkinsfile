pipeline {
    agent any
    
    stages {
        // Stage 1: SonarQube Scan
        stage('SonarQube Scan') {
            steps {
                script {
                    echo "Starting SonarQube analysis..."
                    // Run SonarQube scanner with project configuration
                    withSonarQubeEnv('SonarQube') {
                        bat '''
                            @echo off
                            echo Running SonarQube scan on source code...
                            SonarScanner.bat ^
                                -Dsonar.projectKey=simple-app ^
                                -Dsonar.sources=. ^
                                -Dsonar.host.url=http://localhost:9000 ^
                                -Dsonar.login=YOUR_TOKEN
                        '''
                    }
                }
            }
        }
        
        // Stage 2: Run App
        stage('Run App') {
            steps {
                script {
                    echo "Executing Java application..."
                    // Run the compiled Java application from JAR file
                    bat '''
                        @echo off
                        echo Running the Java application...
                        java -jar App.jar
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Please check the logs."
        }
    }
}
