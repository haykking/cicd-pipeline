pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                nodejs('nodejs-gtool') {
                    sh 'chmod +x scripts/build.sh'
                    sh 'scripts/build.sh'
                }
            }
        }
        stage('Test') {
            steps {
                nodejs('nodejs-gtool') {
                    sh 'chmod +x scripts/test.sh'
                    sh 'scripts/build.sh'
                }
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
