pipeline {
    agent any

    tools {
        maven 'Maven'   // Matches your Jenkins Maven installation
        jdk 'JDK11'     // Matches your Jenkins JDK installation
    }

    environment {
        SONARQUBE = 'SonarQube'  // Matches your SonarQube server name in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/TaherMansourii/devsecops-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                // Waits for the SonarQube quality gate to complete
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment stage - add your deployment steps here'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs!'
        }
    }
}

