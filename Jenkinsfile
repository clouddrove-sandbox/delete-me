pipeline {
    agent {label 'docker-agent-magento2' }
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
                sh 'git version'
                sh 'git pull origin production --no-commit'
                //sh '<BUILD COMMAND>'

            }
        }      
        
          
        stage('Push') {
            steps {    
                sh 'git add .'
                sh 'git status'
                sh 'git commit -m "Jenkins Pipeline build $BRANCH_NAME-$BUILD_NUMBER [ci skip]"'
                sh 'git push origin $BRANCH_NAME'


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
