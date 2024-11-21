pipeline{
  agent any
  stages{
    stage('Enable SSH') {
      steps {
        script {
            // Enable SSH service
            sh '''
            echo "Enabling SSH service..."
            sudo systemctl enable ssh
            sudo systemctl start ssh
            '''
        }
      }
    }
    stage('Create Key') {
      steps {
        sh '''
            if [ ! -f /home/selcia/.ssh/id_rsa ]; then
                echo "Generating SSH key pair..."
                ssh-keygen -t rsa -b 2048 -f /home/selcia/.ssh/id_rsa -N ""
            else
                echo "SSH key already exists. Skipping generation."
            fi
        '''
      }
    }
    stage('Copy Key') {
      steps {
          script {
            // Copy public key to the remote server
            sh '''
            echo "Copying key to remote server..."
            ssh-copy-id -i /home/selcia/.ssh/id_rsa.pub selcia@192.168.119.132 || echo "Key already exists or connection failed"
            '''
        }
      }
    }
    stage('Test SSH Connection'){
      steps {
          script {
              // Test the SSH connection
              sh '''
              echo "Testing SSH connection..."
              ssh selcia@192.168.119.132 uptime
              '''
          }
      }
    }
  }
}
