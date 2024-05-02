pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'git-test',
                    url: 'https://github.com/NOOJU/jenkins-test.git'
            }
        }
    }
}
