pipeline{
  agent any
  stages{
    // stage('Enable SSH') {
    //   steps {
    //     script {
    //         // Enable SSH service
    //         sh '''
    //         echo "Enabling SSH service..."
    //         sudo systemctl enable ssh
    //         sudo systemctl start ssh
    //         '''
    //     }
    //   }
    // }
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
    stage('Prepare File') {
            steps {
                script {
                    // Create a dummy file to transfer
                    sh '''
                    echo "This is a test file for transfer" > /tmp/testfile.txt
                    '''
                }
            }
        }
        stage('Transfer File to Remote Server') {
            steps {
                script {
                    // Transfer the file using scp
                    sh '''
                    echo "Transferring file to remote server..."
                    scp -o StrictHostKeyChecking=no /tmp/testfile.txt selcia@192.168.119.132:/home/selcia/
                    '''
                }
            }
        }
        stage('Verify Transfer') {
            steps {
                script {
                    // Verify the file on the remote server
                    sh '''
                    echo "Verifying file on remote server..."
                    ssh -o StrictHostKeyChecking=no selcia@192.168.119.132 ls -l /home/selcia/testfile.txt
                    '''
                }
            }
        }
  }
}
