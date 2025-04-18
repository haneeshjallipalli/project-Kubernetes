## deploy the app & service 
```
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
```

## deploy NGINX Ingress Controller
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml
```

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



