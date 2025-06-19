pipeline {
    agent any

     environment {
        KUBECONFIG='/Users/anujakadu/.kube/config'
     }
     stages {
       stage('Run kubectl') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'kube-8', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://127.0.0.1:54562') {
                    echo "Connected to k8"
                    sh "kubectl apply -f deployment-service.yaml"
                    
                }
            }
        }
        stage('Verify the Deployment') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'kube-8', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://127.0.0.1:54562') {
                        sh "kubectl get pods -n webapps"
                        sh "kubectl get svc -n webapps"
                }
            }
        }    
        
    }
}
