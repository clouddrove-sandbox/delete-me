pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'git config --global user.email "anmol@clouddrove.com"'
                sh 'git config --global user.name "Anmol"'
                sh 'git pull origin production; echo "$branch_name $BUILD_NUMBER"'
                //sh '<BUILD COMMAND>'

            }
        }
        stage('Push') {
            steps {
                sh 'git add .'
                sh 'git commit -m "Jenkins Pipeline build $branch_name-$BUILD_NUMBER"'
                sh 'git push origin $branch_name'


            }
        }
        // stage('Deploy') {
        //     steps {
        //         sh 'git config --global user.email "anmol@clouddrove.com"'
        //         sh 'git config --global user.name "Anmol"'
        //         sh 'git pull origin production'
        //         //sh '<BUILD COMMAND>'

        //     }
        // }                
    }
}
