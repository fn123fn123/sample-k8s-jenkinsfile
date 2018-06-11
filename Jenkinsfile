podTemplate(label: 'dnscontrolpod', containers: [
    containerTemplate(name: 'docker', image: 'docker', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.0', command: 'cat', ttyEnabled: true)
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ]) {
    node('dnscontrolpod') {

        stage('Preview DNS-Control') {
            container('kubectl') {
                    sh "kubectl run --attach pipeline-dns-control --image=docker-sbx.artifactory.sbx.infra.aws-us-east-1.mlbinfra.net/dnscontrol:latest -n default"
                    sh "sleep 10"
                    sh "kubectl delete deployment pipeline-dns-control -n default"
            }
        }
    }
}
