pipeline {
    agent any
    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev7', 'dev9', 'test1'], description: 'Select the environment')

        // Add a dynamic parameter for deployments based on the selected environment
        activeChoiceReactiveParam('SERVICES_TO_SCALE') {
            description('Select the services to scale')
            choiceType('CHECKBOX')
            groovyScript {
                script("""
                    switch (params.ENVIRONMENT) {
                        case 'dev7':
                            return ['dev7-nike-email', 'dev7-nike-web']
                        case 'dev9':
                            return ['dev9-nike-email', 'dev9-nike-web']
                        case 'test1':
                            return ['test1-nike-email', 'test1-nike-web']
                        default:
                            return []
                    }
                """)
                fallbackScript('return ["No services available"]')
            }
        }
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
                            services_to_scale: "${params.SERVICES_TO_SCALE.split(',').collect { it.trim() }}"
                        ]
                    )
                }
            }
        }
    }
}
