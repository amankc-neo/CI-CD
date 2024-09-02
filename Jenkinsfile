pipeline {
    agent any

environment {
        DOCKER_IMAGE = 'your-username/ci-cd-node-app'
    }

stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/ci-cd-node-app.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'npm test'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    dockerImage.push()
                    dockerImage.run('-d -p 3000:3000')
                }
            }
        }
    }

post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
