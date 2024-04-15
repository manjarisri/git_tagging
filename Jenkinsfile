pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/manjarisri/giit_tagging.git'
        GIT_USERNAME = 'manjarisri'
        GIT_PASSWORD = '#Nanami0307'
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
                    def isMerge = sh(script: 'git log --merges -1 --pretty=%B', returnStdout: true).trim().contains('Merge pull request')

                    if (isMerge) {
                        // Generate and push tag
                        echo "Generating and pushing tag"
                        def tagName = "${env.BRANCH_NAME}-0.0.${env.BUILD_NUMBER}"
                        def repo = GIT_URL.replace("https://", "")
                        sh "git tag -a ${tagName} -m 'Auto-generated tag ${tagName}'"
                        sh "git push https://${env.GIT_USERNAME}:${env.GIT_PASSWORD}@${repo} --tags"
                    } else {
                        echo "No merge detected, skipping tag generation and push"
                    }
                }
            }
        }
    }
}
