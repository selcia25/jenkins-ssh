pipeline{
  agent any
  stages{
    stage('Create Key') {
      steps {
        sh 'ssh-keygen -t rsa -b 2048'
      }
    }
  }
}
