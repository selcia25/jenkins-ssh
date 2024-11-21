pipeline{
  agent any
  stage('Create Key') {
    steps {
      sh 'ssh-keygen -t rsa -b 2048'
    }
  }
}
