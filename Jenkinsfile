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
                    installation: 'ansible server', 
                    inventory: '/var/lib/jenkins/workspace/an/host', 
                    playbook: '/var/lib/jenkins/workspace/an/vrf'
                    )
            }
        }
        
        stage('Playbook check') {
            steps {
                ansiblePlaybook(
                    installation: 'ansible server', 
                    inventory: '/var/lib/jenkins/workspace/an/host', 
                    playbook: '/var/lib/jenkins/workspace/an/vrf_check'
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
