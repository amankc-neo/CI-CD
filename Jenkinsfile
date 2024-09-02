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
               script {
                    dockerImage.push()
                    dockerImage.run('-d -p 3000:3000')
                }
              sh 'docker-compose up -d'
           }
        } 
            

       post {
          always {
              echo 'Pipeline finished.'
        }
    }

}
