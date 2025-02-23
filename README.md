## How to Run

1. Install [Minikube](https://medium.com/@sushantkumarsinha22/kubernetes-setting-up-ingress-on-apple-silicon-mac-m1-5fb6bddcb838)

2. Run Minikube: `minikube start --driver qemu --network socket_vmnet`

3. Enable Ingress Controller: `minikube addons enable ingress`

4. https://medium.com/@cldop.com/deploying-jenkins-on-local-kubernetes-cluster-with-helm-chart-and-argocd-part-2-how-to-setup-d7ffb3170f43
      - Name: `kubernetes`
      - Kubernetes URL: `https://kubernetes.default`
      - WebSocket [x]
      - Jenkins URL: `http://jenkins-service.jenkins.svc.cluster.local:8080`

5. Piplenie Project

```
pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
        '''
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
      }
    }
  }
}
```
[https://medium.com/@cldop.com/deploying-jenkins-on-local-kubernetes-cluster-with-helm-chart-and-argocd-part-2-how-to-setup-d7ffb3170f43]
   
