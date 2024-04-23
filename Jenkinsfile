pipeline {
    agent any
    stages {
        stage('Clone repository') {
            steps {
                script {
                    git branch: 'develop', url: 'https://github.com/LokendraDevOps/Jenkins_Assignmnet.git'
                }
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
