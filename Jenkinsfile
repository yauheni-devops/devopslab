pipeline {
    agent {
        docker {
            image 'lachlanevenson/k8s-kubectl:v1.25.0'
            // Добавляем --net=host, чтобы контейнер унаследовал сеть хост-системы
            args '--entrypoint="" --net=host' 
        }
    }
    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'minikube-config', variable: 'KUBECONFIG')]) {
                    // Добавляем флаг пропуска валидации TLS-сертификата
                    sh 'kubectl apply -f k8s/deployment.yml --insecure-skip-tls-verify=true'
                }
            }
        }
    }
}
