<img width="464" alt="image" src="https://github.com/user-attachments/assets/4d7a4d51-b5a1-4607-913c-ef4da41278eb" />## deploy the app & service 
```
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
```

## Install NGINX Ingress Controller
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.1/deploy/static/provider/cloud/deploy.yaml
```

### It will install the controller in the ingress-nginx namespace, creating that namespace if it doesn’t already exist.

### Expected o/p: Two pods are expected be in completed state as they are for only one time task.

<img width="464" alt="image" src="https://github.com/user-attachments/assets/17c6e59a-67a8-42b0-918e-acb1c9d46739" />


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
## Now hit localhost to access the application
```
localhost
```

## Others:

### Ingress controller installation using Helm
```
helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace
```
