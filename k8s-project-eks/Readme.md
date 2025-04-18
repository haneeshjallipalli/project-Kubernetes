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

# Now follow the instructions in ingress.md file

## Once you are done, cleanup the cluster 
```
eksctl delete cluster --name haneesh-cloud --region us-west-1
```
