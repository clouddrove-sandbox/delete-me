pipeline {
    agent any
    stages {
        stage('Run CI?') {
            steps {
                script {
                if (sh(script: "git log -1 --pretty=%B | fgrep -ie '[skip ci]' -e '[ci skip]'", returnStatus: true) == 0) {
                    currentBuild.result = 'NOT_BUILT'
                    error 'Aborting because commit message contains [skip ci]'
                }
                }
            }
        }        
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
