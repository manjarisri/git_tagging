pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/manjarisri/git_tagging.git'
        GIT_USERNAME = 'manjarisri'
        GIT_PASSWORD = '#Nanami0307'
        MYSQL_STATUS = ''
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
                    def mysqlStatus = sh(script: "bash /home/knoldus/check_env/bashsyn.sh", returnStatus: true)== 0 ? 'running' : 'not running'                    
                }
            }
        }
    }
    post {
        always {
            echo "MySQL is ${env.MYSQL_STATUS} on ${params.DEV_SERVER}."
        }
    }
}
