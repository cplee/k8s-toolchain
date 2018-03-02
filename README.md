# Setup
* brew install kubernetes-helm
* helm init

# TLS
* openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/tls.key -out /tmp/tls.crt -subj "/CN=toolchain-docker-registry"
* sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain /tmp/tls.crt
* kubectl create secret tls toolchain-docker-registry.tls --key /tmp/tls.key --cert /tmp/tls.crt 

# Deploy
* helm dependency update toolchain
* helm install toolchain -f local-values.yml -n toolchain

# Login to Jenkins
* URL: http://localhost:30080
* Username: admin
* Password: `kubectl get secret toolchain-jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 -D`

# View Jenkins logs
* kubectl logs -lcomponent=toolchain-jenkins-master 
