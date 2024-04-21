pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'develop', credentialsId: 'https://github.com/LokendraDevOps/Jenkins_Assignmnet.git' 
            }
        }
    }
    triggers {
        scm {
            branches { "develop" }
        }
    }

    stages {
        stage('Copy to Test Node (if successful)') {
            when {
                expression { return $currentBuild.result == 'SUCCESS' }
            }
            steps {
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

