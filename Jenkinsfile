pipeline {
  agent {
    docker {
      image 'hippolab/ansible'
      args '-u 0:0'
      reuseNode true
    }
  }
  
  environment {
    ANSIBLE_VAULT_PASSWORD = credentials('ANSIBLE_VAULT_PASSWORD')
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
            echo ${ANSIBLE_VAULT_PASSWORD} | ansible-playbook \
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
