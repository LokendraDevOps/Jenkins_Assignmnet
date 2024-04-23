pipeline {
    agent any
    triggers {
        pollSCM 'H/0 * * * *'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'develop']],
                    userRemoteConfigs: [[url: 'https://github.com/LokendraDevOps/Jenkins_Assignmnet.git']]
                    ])
                }
            }         
        
        stage('Copy to Test Node (if successful)') {
            when {
                expression { currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    sh 'rsync -avz -e ssh . 172.31.21.36:/home/ubuntu/Job-3'
                }
            }
        }

        stage('Deploy to Prod (if successful)') {
            when {
                expression { currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    sh 'rsync -avz -e ssh . 172.31.19.138:/home/ubuntu/Job-3'
                }
            }
        }
    }
}
