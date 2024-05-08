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


        stage('Insert autority data into jenkins-server') {
            steps {
                ansiblePlaybook(
                    installation: 'ansible-server', 
                    inventory: '/var/lib/jenkins/workspace/jenkins-test/ansible/hosts', 
                    playbook: '/var/lib/jenkins/workspace/jenkins-test/ansible/playbook/auto_pass.yml'
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


        
        stage('check configuration') {
            steps {
                ansiblePlaybook(
                    installation: 'ansible-server', 
                    inventory: '/var/lib/jenkins/workspace/jenkins-test/ansible/hosts', 
                    playbook: '/var/lib/jenkins/workspace/jenkins-test/ansible/playbook/verify-vlan-vrf.yml'
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
