pipeline{
  agent any
  stages{
    stage('Create Key') {
      steps {
        sh 'ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa -N'
      }
    }
    stage('Copy Key') {
      steps {
          script {
              sh '''
              ssh-copy-id -i ~/.ssh/id_rsa.pub selcia@192.168.119.132 || echo "Key already exists or connection failed"
              '''
          }
      }
    }
  }
}
