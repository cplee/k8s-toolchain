# Setup
* brew install kubernetes-helm
* helm init
* helm install stable/kubernetes-dashboard

# Deploy
* helm dependency update toolchain
* helm install toolchain -f local-values.yml -n toolchain

# Login to Jenkins
* URL: `kubectl get services toolchain-jenkins -o jsonpath='http://localhost:{.spec.ports[0].nodePort}'`
* Username: admin
* Password: `kubectl get secret toolchain-jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 -D`
