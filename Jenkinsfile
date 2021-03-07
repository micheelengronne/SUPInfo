node {
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {
        ansiblePlaybook( 
            playbook: 'playbook.yml',
            inventory: 'hosts', 
            credentialsId: 'sample-ssh-key',
            colorized: true) 
    }
}
