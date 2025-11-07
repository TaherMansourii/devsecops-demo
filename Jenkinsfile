pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from GitHub"
            }
        }

        stage('Build') {
            steps {
                echo 'Building... (simulate build)'
                sh 'mkdir -p build && echo "build artifact" > build/artifact.txt'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Running unit tests (simulate)'
                sh 'echo "ok" > build/test-results.txt'
            }
            post {
                always {
                    archiveArtifacts artifacts: 'build/**', fingerprint: true
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}

