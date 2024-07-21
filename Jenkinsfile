pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') { 
            agent {
                docker {
                    image 'node:lts-buster-slim'
                    args '-p 3000:3000'
                }
            }
            steps {
                sh 'npm start &'
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/deliver.sh' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
