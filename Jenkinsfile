pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'minikube-config', variable: 'KUBECONFIG')]) {
                    sh '''
                        cat $KUBECONFIG | docker run --rm -i \
                          --net=host \
                          -v $PWD:/workspace \
                          -w /workspace \
                          lachlanevenson/k8s-kubectl:v1.25.0 \
                          --kubeconfig=/dev/stdin \
                          apply -f k8s/deployment.yml --insecure-skip-tls-verify=true
                    '''
                }
            }
        }
    }
}
