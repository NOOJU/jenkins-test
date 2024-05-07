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
    }

        stage('Run Ansible Playbook') {
            steps {
                ansiblePlaybook(
                    installation: 'ansible-server', 
                    inventory: '/var/lib/jenkins/workspace/jenkins-test/host', 
                    playbook: '/var/lib/jenkins/workspace/jenkins-test/vrf-vlan-test.yml'
                    )
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
