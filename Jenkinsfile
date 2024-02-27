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
                    sh 'scripts/test.sh'
                }
            }
        }
        stage('Build Docker Image Dev') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    docker.removeImage('nodedev:v1.0')
                    docker.build('nodedev:v1.0', '.')
                }
            }
        }
        stage('Build Docker Image Main') {
            when {
                branch 'main'
            }
            steps {
                script {
                    docker.removeImage('nodemain:v1.0')
                    docker.build('nodemain:v1.0', '.')
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
