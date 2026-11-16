def remote = [:]
remote.name = 'Staging Server'
remote.allowAnyHosts = true

node {
  withCredentials([string(credentialsId: 'ubuntu-staging-server-username', variable: 'STAGING_USERNAME'), string(credentialsId: 'ubuntu-staging-server-host', variable: 'STAGING_HOST'), string(credentialsId: 'ubuntu-staging-server-password', variable: 'STAGING_PASSWORD')]) {
    remote.host = STAGING_HOST
    remote.user = STAGING_USERNAME
    remote.password = STAGING_PASSWORD
    stage('Deploy to staging') {
      sshCommand remote: remote, command: 'cd ~/workspace/jenkins-training && git pull'
    }
  }
}
