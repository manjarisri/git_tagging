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
                // Replace this with your build commands
                sh 'echo "Building..."'
            }
        }

        stage('Test') {
            steps {
                // Replace this with your test commands
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
                        // def branch = sh(script: 'git rev-parse --abbrev-ref HEAD', returnStdout: true).trim()
                        def tagName = "${env.BRANCH_NAME}-0.0.${env.BUILD_NUMBER}"
                        sh "git tag -a ${tagName} -m 'Auto-generated tag ${tagName}'"
                        repo = GIT_URL.replace("https://", "")
                        sh "git push https://${env.GIT_USERNAME}:${env.GIT_PASSWORD}@${repo} --tags"
                    } else {
                        echo "No merge detected, skipping tag generation and push"
                    }
                }
            }
        }
    }
    }  

    

    

