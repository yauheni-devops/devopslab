pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
               withCredentials([string(credentialsId: 'kubeconfig-text', variable: 'KUBECONFIG')]) {
                   sh 'kubectl get nodes'
                    sh 'kubectl apply -f k8s/deployment.yml'
                    sh 'kubectl apply -f k8s/service.yml'
                }
            }
        }
    }
}
