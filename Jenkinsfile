pipeline { 
    agent any 
    parameters {
            choice(name: 'ACTION', choices: ['deploy', 'undeploy'], description: 'Choose action')
        }
    stages {
        stage('Undeploy') {
        when { 
            expression { params.ACTION == 'undeploy' }
        }
        steps {
            sh "az login -i"
            sh "export KUBECONFIG=~/.kube/config"
            sh "kubelogin convert-kubeconfig -l msi"
            sh 'helm uninstall -n elad interview-assignment'
        }
}
        stage('Deploy') {
            when {
                expression { params.ACTION == 'deploy' } 
            }
            steps {
                sh "az login -i"
                sh "export KUBECONFIG=~/.kube/config"
                sh "kubelogin convert-kubeconfig -l msi"
                sh "helm upgrade --install interview-assignment . --values values.yaml -n elad"
            }
        }
    }
}