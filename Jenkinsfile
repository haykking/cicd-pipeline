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
                    containerId = docker.listContainers(filters: ['label=name=nodedev:v1.0'])[0]?.id
                    if (containerId) {
                        docker.stopContainer(containerId)
                        docker.removeContainer(containerId)
                    }
                    docker.build('nodedev:v1.0', '.')
                    sh "docker run -d --expose 3001 -p 3001:3000 nodedev:v1.0"
                }
            }
        }
        stage('Build Docker Image Main') {
            when {
                branch 'main'
            }
            steps {
                script {
                    containerId = docker.listContainers(filters: ['label=name=nodemain:v1.0'])[0]?.id
                    if (containerId) {
                        docker.stopContainer(containerId)
                        docker.removeContainer(containerId)
                    }
                    docker.build('nodemain:v1.0', '.')
                    sh "docker run -d --expose 3000 -p 3000:3000 nodemain:v1.0"
                }
            }
        }
        stage('Deploy') {
            steps {
                docker.withRegistry('https://registry.hub.docker.com/v2/', 'credentials-id') {
                    def customImage = docker.build('nodemain:v1.0')

                    customImage.push()
                }
            }
        }
    }
}
