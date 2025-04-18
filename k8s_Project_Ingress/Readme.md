## deploy the app & service 
```
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
```

## Install NGINX Ingress Controller
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml
```

### It will install the controller in the ingress-nginx namespace, creating that namespace if it doesn’t already exist.

## deploy ingress resource
```
kubectl apply -f ingress.yaml
```

## Wait for it to come up:
```
kubectl get pods -n ingress-nginx
```
or 

## check the name space
```
kubectl get all -n ingress-nginx
```
## Now hit localhost to access the application
```
localhost
```

## Others:

### Ingress controller installation using Helm
```
helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace
```