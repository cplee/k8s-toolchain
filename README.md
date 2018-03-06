# Setup
* brew install kubernetes-helm
* helm init
* helm dependency update toolchain

# TLS
* openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/tls.key -out /tmp/tls.crt -subj "/CN=toolchain-docker-registry"
* kubectl create secret tls toolchain-docker-registry.tls --key /tmp/tls.key --cert /tmp/tls.crt 

# Deploy Locally
* helm install toolchain -f local-values.yml -n toolchain
* URL: http://localhost:30080
* Username: admin
* Password: `kubectl get secret toolchain-jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 -D`

# Deploy AWS
* helm install toolchain -n toolchain
* URL: kubectl get svc toolchain-jenkins -o jsonpath='{ .status.loadBalancer.ingress[0].hostname }'
* Username: admin
* Password: `kubectl get secret toolchain-jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 -D`

# View Jenkins logs
* kubectl logs -lcomponent=toolchain-jenkins-master 
