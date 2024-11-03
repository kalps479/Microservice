pipeline {
    agent any

    stages {
        stage('Deploy to Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName: 'EKS-1',
                    contextName: 'EKS-1',
                    credentialsId: 'ks-token',
                    namespace: 'webapps',
                    serverUrl: 'https://CCBB17EE196C6B4442EFCFE678F2FB19.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh 'kubectl apply -f deployment-service.yml'
                    sleep 60
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName: 'EKS-1',
                    contextName: 'EKS-1',
                    credentialsId: 'ks-token',
                    namespace: 'webapps',
                    serverUrl: 'https://CCBB17EE196C6B4442EFCFE678F2FB19.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh 'kubectl get all -n webapps'
                }
            }
        }
    }
}
