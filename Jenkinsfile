pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/manjarisri/git_tagging.git'
        GIT_USERNAME = 'manjarisri'
        GIT_PASSWORD = '#Nanami0307'
        MYSQL_STATUS = ''
    }    

    stages {
        stage('Detect Merge and Push Tag') {
            steps {
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: 'aws-ssh', keyFileVariable: 'SSH_KEY')]) {
                        env.MYSQL_STATUS = sh(script: "/home/ubuntu/script.sh", returnStatus: true) == 0 ? 'running' : 'not running'
                        echo "Using SSH Key for authentication"
                    }
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
