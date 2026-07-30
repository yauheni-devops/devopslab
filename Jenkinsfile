pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'minikube-config', variable: 'KUBECONFIG')]) {
                    sh '''
                        docker run --rm \
                          --net=host \
                          -v $KUBECONFIG:/tmp/kubeconfig \
                          -e KUBECONFIG=/tmp/kubeconfig \
                          lachlanevenson/k8s-kubectl:v1.25.0 \
                          apply -f k8s/deployment.yml --insecure-skip-tls-verify=true
                    '''
                }
            }
        }
    }
}
