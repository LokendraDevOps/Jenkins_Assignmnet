pipeline {
    agent any

    scm {
        git 'https://github.com/LokendraDevOps/Jenkins_Assignmnet.git' // Corrected URL (assuming HTTPS)
        branch 'develop'
    }

    triggers {
        scm { // This is the correct syntax for SCM trigger
            branches { "develop" }
        }
    }

    stages {
        stage('Copy to Test Node (if successful)') { // More descriptive name
            when {
                expression { return $currentBuild.result == 'SUCCESS' } // Ensure previous stage succeeds
            }
            steps {
                script {
                    sh 'rsync -avz -e ssh . 172.31.21.36:/home/ubuntu/Job-3' // Assuming SSH key-based authentication
                }
            }
        }

        stage('Deploy to Prod (if successful)') {
            when {
                expression { return $currentBuild.result == 'SUCCESS' } // Ensure previous stage succeeds
            }
            steps {
                script {
                    sh 'rsync -avz -e ssh . 172.31.19.138:/home/ubuntu/Job-3' // Assuming SSH key-based authentication
                }
            }
        }
    }
}
