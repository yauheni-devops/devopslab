pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'minikube-config', variable: 'KUBECONFIG')]) {
                    sh 'kubectl apply -f k8s/deployment.yml --insecure-skip-tls-verify=true'
                }
            }
        }
    }
}
