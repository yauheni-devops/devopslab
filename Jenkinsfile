pipeline {
    agent any

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'minikube-config', variable: 'KUBECONFIG')]) {
                    sh '''
                        docker run --rm -i \
                          --net=host \
                          -e KUBE_CONFIG="$(cat $KUBECONFIG)" \
                          -e DEPLOY_SPEC="$(cat k8s/deployment.yml)" \
                          --entrypoint /bin/sh \
                          lachlanevenson/k8s-kubectl:v1.25.0 \
                          -c 'echo "$KUBE_CONFIG" | kubectl --kubeconfig=/dev/stdin apply -f - --insecure-skip-tls-verify=true <<EOF
$DEPLOY_SPEC
EOF'
                    '''
                }
            }
        }
    }
}
