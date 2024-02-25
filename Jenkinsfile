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
                sh 'scripts/test.sh'
            }
        }
        stage('Build Docker Image Dev') {
            when {
                branch: 'dev'
            }
            agent {
                docker { image 'node:7.8.0' }
            }
        }
        stage('Build Docker Image Main') {
            when {
                branch: 'main'
            }
            agent {
                docker { image 'node:7.8.0' }
            }
        }
        stage('Deploy') {
            steps {
                // Add deployment steps here
            }
        }
    }
}
