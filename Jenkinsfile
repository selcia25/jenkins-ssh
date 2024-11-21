pipeline{
  agent any
  stages{
    stage('Create Key') {
      steps {
        sh 'ssh-keygen -t rsa -b 2048 -f /home/selcia/.ssh/id_rsa -N "" -q <<< y'
      }
    }
    stage('Copy Key') {
      steps {
          script {
              sh '''
            if [ ! -f /home/selcia/.ssh/id_rsa ]; then
                ssh-keygen -t rsa -b 2048 -f /home/selcia/.ssh/id_rsa -N ""
            fi
                '''
          }
      }
    }
  }
}
