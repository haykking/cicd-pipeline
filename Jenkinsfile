pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Tool Install') {
            steps {
                nodejs 'nodejs-gtool'
            }
        }
        stage('Build') {
            steps {
                sh 'chmod +x scripts/build.sh'
                sh 'scripts/build.sh'
            }
        }
        stage('Test') {
            steps {
                sh 'chmod +x scripts/test.sh'
                sh 'scripts/test.sh'
            }
        }
        stage('Build Docker Image Dev') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    docker.build('nodemain:v1.0', './Dockerfile')
                }
            }
        }
        stage('Build Docker Image Main') {
            when {
                branch 'main'
            }
            steps {
                script {
                    docker.build('nodedev:v1.0', './Dockerfile')
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Add deployment steps here'
            }
        }
    }
}
