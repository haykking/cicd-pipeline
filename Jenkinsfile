pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'scripts/build.sh'
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
            steps {
                docker.build('nodemain:v1.0', './Dockerfile')
            }
        }
        stage('Build Docker Image Main') {
            when {
                branch: 'main'
            }
            steps {
                docker.build('nodedev:v1.0', './Dockerfile')
            }
        }
        stage('Deploy') {
            steps {
            // Add deployment steps here
            }
        }
    }
}
