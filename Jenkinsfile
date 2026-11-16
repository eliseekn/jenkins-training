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

                withCredentials(bindings: [sshUserPrivateKey(credentialsId: 'ubuntu-staging-server')]) {
                  sh 'cd ~/workspace/jenkins-training && git pull'
                }
            }
        }
    }
}
