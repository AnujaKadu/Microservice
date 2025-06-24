pipeline {
    agent any

     environment {
        KUBECONFIG='/Users/anujakadu/.kube/config'
     }
     stages {
       stage('Run kubectl') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'kind-kind-multi-node', contextName: '', credentialsId: 'kube-8', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://127.0.0.1:49226') {
                    echo "Connected to k8"
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        stage('Verify the Deployment') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kind-kind-multi-node', contextName: '', credentialsId: 'kube-8', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://127.0.0.1:49226') {
                        sh "kubectl get pods -n webapps"
                        sh "kubectl get svc -n webapps"
                }
            }
        }    
        
    }
}
