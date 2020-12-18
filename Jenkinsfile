pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world!"'
                sh 'git config --global user.email "anmol@clouddrove.com"'
                sh 'git config --global user.name "Anmol"'
                sh 'git pull origin production'
                sh 'cat printme.txt'
            }
        }
    }
}
