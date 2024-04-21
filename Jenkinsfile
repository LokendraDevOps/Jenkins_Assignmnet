pipeline {
    agent any

    triggers {
        scm {
            branches { "develop" }
        }
    }

    stages {
        stage('Copy to Test Node') {
            steps {
                sh 'git checkout . && git pull' (branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/LokendraDevOps/Jenkins_Assignmnet.git']])
                script {
                    sh 'rsync -avz -e ssh . 172.31.21.36:/home/ubuntu/Job-3'
                }
            }
        }
        stage('Deploy to Prod (if successful)') {
            when {
                expression { return $currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    sh 'rsync -avz -e ssh . 172.31.19.138:/home/ubuntu/Job-3'
                }
            }
        }
    }
}