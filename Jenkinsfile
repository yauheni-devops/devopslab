pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([string(credentialsId: 'kubeconfig-content', variable: 'KUBECONFIG_RAW')]) {
                    script {
                        // Создаём файл kubeconfig из переменной
                        sh 'echo "$KUBECONFIG_RAW" > kubeconfig'
                        // Используем этот файл
                        sh 'kubectl --kubeconfig kubeconfig get nodes'
                        sh 'kubectl --kubeconfig kubeconfig apply -f k8s/deployment.yml'
                        sh 'kubectl --kubeconfig kubeconfig apply -f k8s/service.yml'
                    }
                }
            }
        }
    }
}
