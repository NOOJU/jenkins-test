pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github_token',
                    url: 'https://github.com/NOOJU/jenkins-test.git'
            }
        }


        stage('Run autority-pass Playbook') {
            steps {
                ansiblePlaybook(
                    installation: 'ansible-server', 
                    inventory: '/var/lib/jenkins/workspace/jenkins-test/ansible/hosts', 
                    playbook: '/var/lib/jenkins/workspace/jenkins-test/ansible/playbook/auto-pass.yml'
                    )
            }
        }


        
        stage('Run config Playbook') {
            steps {
                ansiblePlaybook(
                    installation: 'ansible-server', 
                    inventory: '/var/lib/jenkins/workspace/jenkins-test/ansible/hosts', 
                    playbook: '/var/lib/jenkins/workspace/jenkins-test/ansible/playbook/vrf-vlan-test.yml'
                    )
            }
        }

    }
        
    post {
        success {
            echo 'Playbook executed successfully!'
        }
        failure {
            echo 'Playbook execution failed!'
        }
    }
}     
