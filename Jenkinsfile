pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'app/build/libs/**/*.jar', fingerprint: true
            junit allowEmptyResults: true, testResults: 'app/build/reports/**/*.xml'
        }
    }
}