pipeline {
    agent any

environment {
        DOCKER_IMAGE = 'sampleapp/v2'
    }

stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/amankc-neo/CI-CD.git'
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
              sh 'docker-compose up -d'
           }
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
