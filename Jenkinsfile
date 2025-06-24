pipeline {
    agent any

     environment {
        KUBECONFIG='/Users/anujakadu/.kube/config'
        KUBERNETES_URL='https://127.0.0.1:545'
        NAMESPACE= 'webapps'
        KUBERNETES_CREDENTIALS_ID= 'kube-8' 
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
                    //sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        stage('Verify the Deployment') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: KUBERNETES_CREDENTIALS_ID, namespace: NAMESPACE, restrictKubeConfigAccess: false, serverUrl: KUBERNETES_URL) {
                        sh "kubectl get pods -n webapps"
                        sh "kubectl get svc -n webapps"
                }
            }
        }    
        
    }
}
