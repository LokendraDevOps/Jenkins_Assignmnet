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
                    // Use appropriate tools (e.g., rsync, SCP) to copy files to the test node
                    // Replace 'test_node_ip' and '/path/to/test/directory' with your actual values
                    sh 'rsync -avz -e ssh . 172.31.21.36:/home/ubuntu/Job-3'
                }
            }
        }
        stage('Test') {
            steps {
                // Define your test execution commands here
                // Example: run shell script, unit tests, etc.
                sh 'sh /path/to/test_script.sh'
            }
        }
        stage('Deploy to Prod (if successful)') {
            when {
                expression { return $currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    // Use appropriate tools to copy files to the prod node
                    // Replace 'prod_node_ip' and '/path/to/prod/directory' with your actual values
                    sh 'rsync -avz -e ssh . 172.31.19.138:/home/ubuntu/Job-3'
                }
            }
        }
    }
