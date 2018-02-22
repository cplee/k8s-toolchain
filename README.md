# Setup
* brew install kubernetes-helm
* helm init

# Deploy
* helm dependency update clair
* helm install clair -f clair-values.yml

