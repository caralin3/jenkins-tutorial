pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project...'
                git branch: 'master'
                    credentialsId: 'git-hub-key'
                    url: 'ssh://git@github.com:caralin3/jenkins-test-sync.git'
                sh 'ls pwd'
            }
        }
        stage('Build') {
            steps {
                script {
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
        }
        stage('Test') {
            steps {
                script {
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
    }
    post {
        always {
            archiveArtifacts artifacts: 'app/build/libs/**/*.jar', fingerprint: true
            junit allowEmptyResults: true, testResults: 'app/build/reports/**/*.xml'
        }
    }
}