pipeline {
    agent any
    stages {
//         stage('Build') {
//             steps {
//                 sh './gradlew build'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './gradlew test'
//             }
//         }
        stage('Checkout') {
            steps {
                echo 'Cloning project...'
                sh 'git clone --single-branch --branch master git@github.com:caralin3/jenkins-test-sync.git'
            }
        }
        stage('Build') {
            steps {
                dir("jenkins-test-sync") {
                    try {
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
            dir("jenkins-test-sync") {
                try {
                    sh './gradlew test'
                }
                catch(Exception e) {
                    echo 'Error ${e.getMessage()} occurred.'
                    e.printStackTrace();
                }
            }
        }
//         stage('Cleanup') {
//             steps {
//                 cleanWs();
//             }
//         }
    }
    post {
        always {
            archiveArtifacts artifacts: 'app/build/libs/**/*.jar', fingerprint: true
            junit allowEmptyResults: true, testResults: 'app/build/reports/**/*.xml'
        }
    }
}