pipeline {
  agent {
    docker {
      image 'williamyeh/ansible:ubuntu14.04'
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
            ansible-galaxy install -r requirements.yml
            ansible-playbook \
              --inventory-file hosts \
              --extra-vars ansible_ssh_common_args='"-o StrictHostKeyChecking=no -o ServerAliveInterval=30"' \
              --ask-vault-pass \
              playbook.yml
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
