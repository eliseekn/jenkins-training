pipeline {
  agent any

  options {
    timeout(time: 10, unit: 'MINUTES')
    disableConcurrentBuilds()
  }

  environment {
    APP_DIR = '~/workspace/jenkins-training'
    KNOWN_HOSTS = '/var/lib/jenkins/.ssh/known_hosts'
  }

  stages {
    stage('Test') {
      steps {
        echo 'Runing tests...'
      }
    }

    stage('Deploy to staging') {
      when { branch 'develop' }

      steps {
        withCredentials([
          string(credentialsId: 'ubuntu-staging-server-host', variable: 'STAGING_HOST'),
          sshUserPrivateKey(
            credentialsId: 'staging-ssh-key',
            keyFileVariable: 'SSH_KEY',
            usernameVariable: 'SSH_USER'
          )
        ]) {
          sh 'ssh -i "$SSH_KEY" -o BatchMode=yes -o StrictHostKeyChecking=yes -o UserKnownHostsFile="$KNOWN_HOSTS" "$SSH_USER@$STAGING_HOST" "cd $APP_DIR && git pull"'
        }
      }
    }
  }

  post {
    success {
      echo 'Deploy to staging succeeded'
    }
    failure {
      echo 'Deploy failed'
    }
  }
}
