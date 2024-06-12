pipeline {
    agent any
    parameters {
        extendedChoice(
            name: 'SERVICES_TO_SCALE',
            type: 'PT_CHECKBOX',
            description: 'Select the services to scale',
            multiSelectDelimiter: ',',
            value: 'my-dep,nginx-deployment'
        )
        choice(name: 'NAMESPACE', choices: 'manjari', description: 'Namespace of the services')
    }

    environment {
        GIT_URL = 'https://github.com/manjarisri/git_tagging.git'
        GIT_USERNAME = 'manjarisri'
        GIT_PASSWORD = '#Nanami0307'
        // KUBECONFIG = credentials('minikube')
    }

    stages {
        stage('Deploy to k8s') {
            steps {
                dir("${workspace}/kube") {
                    ansiblePlaybook(
                        playbook: './playbook.yaml',
                        inventory: './hosts/inventory',
                        credentialsId: 'KUBECONFIG',
                        extras: '-vvv',
                        extraVars: [
                            namespace: "${params.NAMESPACE}",
                            SERVICES_TO_SCALE: "${params.SERVICES_TO_SCALE.split(',').collect { it.trim() }}"
                        ]
                    )
                }
            }
        }
    }
}
