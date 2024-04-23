pipeline {
    agent any

    triggers {
        pollSCM '*/02 * * * *' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'develop']],
                    userRemoteConfigs: [[url: 'https://github.com/LokendraDevOps/Jenkins_Assignmnet.git']]
                ])
                } catch (err) {
                    echo "Error during checkout: ${err.message}"
                    currentBuild.result = 'FAILURE'
                }
            }      
        stage('Copy to Test Node (if successful)') {
            when {
                expression { currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    sh 'rsync -avz -e ssh .  it@192.168.1.207:/home/it/Pictures'
                }
            }
        }

        stage('Deploy to Prod (if successful)') {
            when {
                expression { currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    sh 'rsync -avz -e ssh .  it@192.168.1.207:/home/it/Pictures' 
                }
            }
        }
    }
}
