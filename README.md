# Setup
* brew install kubernetes-helm
* helm init
* helm dependency update toolchain

# Deploy Locally
* helm install toolchain -f local-values.yml -n toolchain
* URL: http://localhost:30080
* Username: admin
* Password: `kubectl get secret toolchain-jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 -D`

# Deploy AWS
* helm install toolchain -n toolchain
* URL: `kubectl get svc toolchain-jenkins -o jsonpath='{ .status.loadBalancer.ingress[0].hostname }'`
* Username: admin
* Password: `kubectl get secret toolchain-jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 -D`