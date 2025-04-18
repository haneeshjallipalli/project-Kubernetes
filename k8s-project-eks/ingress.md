## deploy the app & service 
```
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
```

## Install NGINX Ingress Controller
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.1/deploy/static/provider/aws/deploy.yaml
```

### It will install the controller in the ingress-nginx namespace, creating that namespace if it doesn’t already exist.

## Wait for it to come up:
```
kubectl get pods -n ingress-nginx
```

## deploy ingress resource
```
kubectl apply -f ingress.yaml
```

## check the name space
```
kubectl get all -n ingress-nginx
```
## get the dns/ip address & hit it access your application
```
kubectl get ingress
```

## Others:

### Ingress controller installation using Helm
```
helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace
```