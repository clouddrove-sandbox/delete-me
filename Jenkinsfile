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
                sshagent(['101ac0de-323a-4789-bc5f-24e500645924']){
                sh 'git config --global user.email "anmol@clouddrove.com"'
                sh 'git config --global user.name "Anmol"'
                sh 'git checkout $BRANCH_NAME; git pull '
                sh 'git pull origin production --no-commit'
                    
                //sh 'php bin/magento setup:static-content:deploy'
                }
            }
        }      
        
        stage('Push') {
            steps {    
                sh 'git add .'
                sh 'git status'
                sh 'git commit -m "Jenkins Pipeline build $BRANCH_NAME-$BUILD_NUMBER [ci skip]"'
                sh 'git push origin $BRANCH_NAME;'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(credentials : ['use-the-id-from-credential-generated-by-jenkins']) {
                    sh 'ssh  -p 15873 salesstostage_dk@$SERVER_IP "bin/magento maintenance:enable;bin/magento maintenance:status"'
                    sh 'ssh  -p 15873 salesstostage_dk@$SERVER_IP "git clone -b $REPO_URL"'
                    //Premisions etc
                    sh 'ssh  -p 15873 salesstostage_dk@$SERVER_IP "bin/magento maintenance:disable;bin/magento maintenance:status"'
                 
                }
            }
        }                
    }
}
