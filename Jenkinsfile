podTemplate(label: 'label', cloud: 'openshift', serviceAccount: 'appsody-sa', containers: [
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl', ttyEnabled: true, command: 'cat')
                          envVars: [
                                envVar(key: 'IMAGENAME', value: 'appsodyjava'),
                               envVar(key: 'PROJECT', value: 'kabanero')])

  ]){
    node('label') {
        stage('Deploy') {
            container('kubectl') {
                checkout scm
                sh 'sed -i -e \'s#applicationImage: .*$#applicationImage: image-registry.openshift-image-registry.svc:5000/\'$PROJECT\'/\'$IMAGENAME\'#g\' app-deploy.yaml'
                sh 'cat app-deploy.yaml'
                sh 'find . -name app-deploy.yaml -type f|xargs kubectl apply -f'
            }
        }
    }
}
