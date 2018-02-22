# Setup
* brew install kubernetes-helm
* helm init
* helm install stable/kubernetes-dashboard
* helm install stable/nginx-ingress

# Deploy
* helm dependency update clair
* helm install clair -f clair-values.yml

