pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/manjarisri/git_tagging.git'
        GIT_USERNAME = 'manjarisri'
        GIT_PASSWORD = '#Nanami0307'
        REPO_NAME = "${env.JOB_NAME.split('/')[0]}"  // Extract the repo name from the JOB_NAME
        BRANCH_NAME = "${env.JOB_NAME.split('/')[1]}"  // Extract the branch name from the JOB_NAME
    }    

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building..."'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Testing..."'
            }
        }

        stage('Detect Merge and Push Tag') {
            steps {
                script {
                    // Check if a merge to the target branch has occurred
                    // def isMerge = sh(script: 'git log --merges -1 --pretty=%B', returnStdout: true).trim().contains('Merge pull request')
                    echo "${REPO_NAME}_${BRANCH_NAME}"
                    
                }
            }
        }
    }
}
