# Legge til helm repo for offisielle nginx controller
helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update


# Installere ingress controlleren
helm install nginx nginx-stable/nginx-ingress -f values.yaml


# Installere app
kubectl apply -f cafe.yaml

# Sette opp tls
kubectl apply -f cafe-secret.yaml

# Lage virtualserver ressurs
kubectl apply -f cafe-virtual-server.yaml

# Sjekke at virtualservice svarer
curl -kLH "Host: cafe.example.com" https://xx.xx.xx.xx/coffee
curl -kLH "Host: cafe.example.com" https://xx.xx.xx.xx/tea

# FOr jenkins 
add jenkins.example.com in your hostsfile. Use ip for loadbalancer in ingress controllers service