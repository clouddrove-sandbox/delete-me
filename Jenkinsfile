pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world!"'
                sh 'git pull origin production'
                sh 'cat printme.txt'
            }
        }
    }
}
