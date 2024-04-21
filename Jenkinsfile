pipeline {
    agent any
    scm {
        git 'hhttps://github.com/LokendraDevOps/Jenkins_Assignmnet.git'
        branch 'develop'
    }
    triggers {
        scm { 
            branches { "develop" }
        }
        stage('Deploy to test (if successful)') {    
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