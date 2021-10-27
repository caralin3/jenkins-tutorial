pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project...'
                sh 'git clone --single-branch --branch master git@github.com:caralin3/jenkins-test-sync.git'
            }
        }
        stage('Build') {
            steps {
                try {
                    sh 'cd jenkins-test-sync'
                    sh './gradlew build'
                }
                catch(Exception e) {
                    echo 'Error ${e.getMessage()} occurred.'
                    e.printStackTrace();
                }
            }
        }
        stage('Test') {
            steps {
                try {
                    sh 'cd jenkins-test-sync'
                    sh './gradlew test'
                }
                catch(Exception e) {
                    echo 'Error ${e.getMessage()} occurred.'
                    e.printStackTrace();
                }
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