pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world!"'
                sh 'git config --global user.email "anmol@clouddrove.com" ; git pull origin production'
                sh 'cat printme.txt'
            }
        }
    }
}
