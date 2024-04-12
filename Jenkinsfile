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

         stage('Tag') {
            steps {
                echo "Generating and pushing tag for branch: ${env.BRANCH_NAME}"
                script {
                    // Extract event type and branch from the GitHub payload
                    def eventType = env.CHANGE_EVENT
                    def branch = env.CHANGE_BRANCH

                    if (eventType == 'pull_request' && branch == 'dev') {
                        echo "Webhook received for a merge into the dev branch. Proceeding with tag generation."

                        // Generate and push tag
                        echo "Generating and pushing tag for branch: ${branch}"
                        def tagName = "DEV-0.0.${env.BUILD_NUMBER}"
                        sh "git tag -a ${tagName} -m 'Auto-generated tag ${tagName}'"
                        def repoUrl = ${GIT_URL}
                        repo = repoUrl.replace("https://", "")
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${repo} --tags"
                        
                    } else {
                        echo "Webhook received, but not for a merge into the dev branch. Skipping tag generation."
                    }
                }
         
                }
            }
    }  
}

