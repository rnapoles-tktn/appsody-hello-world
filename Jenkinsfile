podTemplate(label: 'label', cloud: 'openshift', serviceAccount: 'appsody-sa', containers: [
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl', ttyEnabled: true, command: 'cat')
  ]){
    node('label') {
        stage('Deploy') {
            container('kubectl') {
                checkout scm
                sh 'sed -i -e \'s#applicationImage: .*$#applicationImage: docker-registry.default.svc:5000/kabanero/java-microprofile#g\' app-deploy.yaml'
                sh 'cat app-deploy.yaml'
                sh 'find . -name app-deploy.yaml -type f|xargs kubectl apply -f'
            }
        }
    }
}
