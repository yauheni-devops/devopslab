pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([string(credentialsId: 'kubeconfig-base64', variable: 'KUBECONFIG_B64')]) {
                    script {
                        sh 'echo "$KUBECONFIG_B64" | base64 -d > kubeconfig'
                        sh 'chmod 600 kubeconfig'
                        sh 'kubectl --kubeconfig kubeconfig get nodes'
                        sh 'kubectl --kubeconfig kubeconfig apply -f k8s/deployment.yml'
                        sh 'kubectl --kubeconfig kubeconfig apply -f k8s/service.yml'
                    }
                }
            }
        }
    }
}
