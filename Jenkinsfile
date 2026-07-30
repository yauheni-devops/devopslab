pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'minikube-config', variable: 'KUBECONFIG')]) {
                    sh '''
                        cat $KUBECONFIG | docker run --rm -i \
                          --net=host \
                          -e DEPLOY_MANIFEST="$(cat k8s/deployment.yml)" \
                          --entrypoint /bin/sh \
                          lachlanevenson/k8s-kubectl:v1.25.0 \
                          -c "echo \\"$DEPLOY_MANIFEST\\" > /tmp/deploy.yaml && kubectl apply -f /tmp/deploy.yaml --kubeconfig=/dev/stdin --insecure-skip-tls-verify=true"
                    '''
                }
            }
        }
    }
}
