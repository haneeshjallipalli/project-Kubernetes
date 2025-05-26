# Steps:
```
Create IAM user with admin access, store the generated access key & Secret Key
Create EC2 instance & login or use any terminal
Install/Upgrade AWS CLI (version2)
Install eksctl
Install Kubectl --> 1.29
aws configure
 >> access key 
 >> secret Key
 >> us-west-1
```

## AWS CLI:
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

## kubectl:
```
sudo curl --silent --location -o /usr/local/bin/kubectl \
"https://dl.k8s.io/release/$(curl --silent --location https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo chmod +x /usr/local/bin/kubectl
```

## eksctl:
```
sudo curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

## apply the following command to create cluster
```
eksctl create cluster -f eks-cluster-config.yaml
```

## deploy the app & service 
```
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
```

## Install NGINX Ingress Controller
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.1/deploy/static/provider/aws/deploy.yaml
```

### Note: It will install the controller in the ingress-nginx namespace, creates the namespace if it doesn’t already exist.
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
## get the dns/ip address with the following command & hit it to access your application
```
kubectl get ingress
```

## Once you are done, cleanup the cluster 
```
eksctl delete cluster --name haneesh-cloud --region us-west-1
```

### Ingress controller installation using Helm (optional)
```
helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace
```
