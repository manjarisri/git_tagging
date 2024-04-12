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

                    // Generate tag name
                    def tagName = "DEV-0.0.${env.BUILD_NUMBER}"

                    // Tag the commit
                    sh "git tag -a ${tagName} -m 'Auto-generated tag ${tagName}'"

                    // Push the tag to the remote repository using withCredentials
                    def repoUrl = "${env.GIT_URL}".replace("https://", "")
                    sh "git push https://${env.GIT_USERNAME}:${env.GIT_PASSWORD}@${env.GIT_URL} --tags"

                    }
         }
                }
            }
        
}

