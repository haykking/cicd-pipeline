pipeline {
    agent none
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Build') {
            steps {
                // Add build steps here
            }
        }

        stage('Test') {
            steps {
                // Add test steps here
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
