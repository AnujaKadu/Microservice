pipeline {
    agent any

     environment {
        KUBECONFIG='/Users/anujakadu/.kube/config'
        KUBERNETES_URL='https://127.0.0.1:54562'
        NAMESPACE= 'webapps'
        KUBERNETES_CREDENTIALS_ID = 'kube-8' 
     }
     stages {
       stage('Run kubectl') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'kind-kind-multi-node', contextName: '', credentialsId: KUBERNETES_CREDENTIALS_ID, namespace: NAMESPACE, restrictKubeConfigAccess: false, serverUrl: KUBERNETES_URL) {
                    echo "Connected to k8"
                    sh "kubectl apply -f deployment-service.yaml"
                    
                }
            }
        }
        stage('Verify the Deployment') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kind-kind-multi-node', contextName: '', credentialsId: KUBERNETES_CREDENTIALS_ID, namespace: NAMESPACE, restrictKubeConfigAccess: false, serverUrl: KUBERNETES_URL) {
                        sh "kubectl get pods -n webapps"
                        sh "kubectl get svc -n webapps"
                }
            }
        }    
        
    }
}
