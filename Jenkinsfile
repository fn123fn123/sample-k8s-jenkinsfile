podTemplate(label: 'mypod', containers: [
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.0', command: 'cat', ttyEnabled: true)
  ]) {
    node('mypod') {

        stage('dnscontrol-preview ') {
          when {
            branch 'PR-*'
          }
            container('kubectl') {
                    sh "kubectl run --attach preview-dns-control --image=docker-sbx.artifactory.sbx.infra.aws-us-east-1.mlbinfra.net/dnscontrol:latest -n default"
                    sh "kubectl delete deployment preview-dns-control -n default"
            }
        }

        stage('dnscontrol-apply') {
          when {
            branch 'master'
          }
            container('kubectl') {
                    sh "kubectl run --attach apply-dns-control --image=docker-sbx.artifactory.sbx.infra.aws-us-east-1.mlbinfra.net/dnscontrol:latest -n default"
                    sh "kubectl delete deployment apply-dns-control -n default"
            }
        }

    }
}
