pipeline {
    agent any

     environment {
        KUBECONFIG= '/Users/anujakadu/.kube/config'
        KUBERNETES_URL= 'https://127.0.0.1:57253'
        NAMESPACE= 'test'
        KUBERNETES_CREDENTIALS_ID= 'kind-kubeconfig' 
        PATH = "/usr/local/bin:$PATH"
     }
     stages {
        stage('Check kubectl') {
            steps {
                sh '''
                    echo "Checking kubectl availability..."
                    which kubectl || echo "kubectl not found"
                    echo "PATH: $PATH"
                '''
            }
        }
       stage('Run kubectl') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: KUBERNETES_CREDENTIALS_ID, namespace: NAMESPACE, restrictKubeConfigAccess: false, serverUrl: KUBERNETES_URL) {
                    echo "Connected to k8"
                    sh "kubectl version"
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        stage('Verify the Deployment') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kind-test', contextName: '', credentialsId: KUBERNETES_CREDENTIALS_ID, namespace: NAMESPACE, restrictKubeConfigAccess: false, serverUrl: KUBERNETES_URL) {
                        sh "kubectl get pods -n NAMESPACE"
                        sh "kubectl get svc -n NAMESPACE"
                }
            }
        }    
        
    }
}
