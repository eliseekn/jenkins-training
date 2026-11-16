pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }

        stage('Deploy to staging') {
            steps {
                echo 'Deploying....'

                withCredentials([sshUserPrivateKey(credentialsId: 'ubuntu-staging-server', keyFileVariable: 'SSH_KEY', usernameVariable: 'USERNAME')]) {
                  echo SSH_KEY
                  echo USERNAME
                }
            }
        }
    }
}
