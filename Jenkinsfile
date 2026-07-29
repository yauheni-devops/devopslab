pipeline {
    agent {
        docker {
            image 'lachlanevenson/k8s-kubectl:v1.25.0'
        }
    }

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-kind', variable: 'KUBECONFIG')]) {
                    sh 'kubectl get nodes'
                    sh 'kubectl apply -f k8s/deployment.yml'
                    sh 'kubectl apply -f k8s/service.yml'
                }
            }
        }
    }
}
