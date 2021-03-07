pipeline {
  agent {
    docker {
      image 'willhallonline/ansible:2.10-ubuntu-20.04'
    }
  }

  options {
    timeout(time: 60, unit: "MINUTES")
  }

  stages {
    stage('Run Ansible playbook') {
      steps {
        sshagent(credentials : ['MY_SSH_KEY_SECRET_ID']) {
          sh '''
            current_path="$PWD"
            cd ../
            ansible-playbook \
              --inventory-file "$current_path"/hosts \
              --extra-vars ansible_ssh_common_args='"-o StrictHostKeyChecking=no -o ServerAliveInterval=30"' \
              "$current_path"/playbook.yml
          '''
        }
      }
    }
  }

  post {
    always {
      deleteDir()
    }
  }

}
