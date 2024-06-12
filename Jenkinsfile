pipeline {
    agent any
    parameters{
        extendedChoice(
            name: 'SERVICES_TO_SCALE',
            type: 'PT_CHECKBOX',
            description: 'Select the services to scale',
            multiSelectDelimiter: ',',
            value: 'service1,service2,service3,service4,service5,service6,service7,service8,service9,service10,service11,service12'
        )    
    }

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
                        env.MYSQL_STATUS = sh(script: """
                        ls -l
                        'bash /home/ubuntu/script.sh'
                        """, returnStatus: true) == 0 ? 'running' : 'not running'
                        echo "Using SSH Key for authentication"
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
