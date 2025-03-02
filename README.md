# Notes for Ultimate DevOps Project and Resume Preparation Udemy Course

- This repository contains the complete notes for the Ultimate DevOps Project and Resume Preparation course prepared by `Abhishek Veeramalla` on Udemy.

- Documentation is organized in Sections, the same way how videos are organized in the udemy course.

- First I created EC2 instance

- ssh -i opentelemetry-keypair-uswest2.pem ubuntu@54.244.87.69

- Install kubectl binary with curl on Linux
-    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
- Validate the binary (optional)
-   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
-   echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
- ![image](https://github.com/user-attachments/assets/2b3edd8a-97ff-42a5-a2d4-2176d7bd5e23)
- 
Install kubectl
  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
  kubectl version --client
  ![image](https://github.com/user-attachments/assets/3dd5ef59-3cde-4324-83b5-f0733fe004eb)



Terraform install https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

  sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

  wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list


sudo apt update

sudo apt-get install terraform

terraform -help
terraform --version

![image](https://github.com/user-attachments/assets/ea94131e-f4d3-455f-a022-e5b9e91b126a)


Git installation 
   sudo apt install git-all
   git clone ..

Install aws cli

  sudo apt update && sudo apt install unzip -y

  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

aws --version

![image](https://github.com/user-attachments/assets/c3c48036-ad74-4d0a-8036-80f553db2902)

aws configure

  AWS Access Key ID [None]: YOUR_ACCESS_KEY
  AWS Secret Access Key [None]: YOUR_SECRET_KEY
  Default region name [None]: us-west-2  # Change to us-west-2
  Default output format [None]: json

Create S3 bucket
  terraform-eks-state-bucket-kani
Create Dynomo db table
  ![image](https://github.com/user-attachments/assets/a9b9a91c-c192-4c1a-bed2-4736a76192e9)

  Terraform init

  ![image](https://github.com/user-attachments/assets/6ed7356b-baa8-438d-aad0-0d09a17ea03c)
  
  Terraform plan
  
  Terraform apply

![image](https://github.com/user-attachments/assets/8fcd982f-0739-4ad1-979d-a6eb9c030899)


once vpc and eks is installed check on aws
VPC

![image](https://github.com/user-attachments/assets/bf4c3836-1b6f-445d-821d-997711acafe7)

EKS
![image](https://github.com/user-attachments/assets/dcd2d4bf-0fdf-4e7b-a409-255c1aefa593)


connect kubectl to the eks cluster

kubectl config view 

kubectl config current-context

![image](https://github.com/user-attachments/assets/e030849b-d936-420e-9f95-cf5f360088b7)


aws eks update-kubeconfig --region <your-region> --name <your-cluster-name>
aws eks update-kubeconfig --region us-west-2 --name my-eks-cluster


kubectl config current-context

![image](https://github.com/user-attachments/assets/0341233c-3e91-48fe-bec1-79a3bd7d3db2)

kubectl get sa

![image](https://github.com/user-attachments/assets/64ff9b1e-ecea-4023-9491-aabfca8b088c)

 kubectl apply -f complete-deploy.yaml
 kubectl get po
![image](https://github.com/user-attachments/assets/f39e173f-f6e9-43cf-9850-0e8ba8f9bff3)

We can access these app if we change the frontendproxy to loadbalancer - but that not a best practise we can use ingress controller to access the main page

commands to configure IAM OIDC provider

 export cluster_name=my-eks-cluster

 oidc_id=$(aws eks describe-cluster --name $cluster_name --query "cluster.identity.oidc.issuer" --output text | cut -d '/' -f 5)

![image](https://github.com/user-attachments/assets/940454f3-8f70-4d68-b333-46271368634a)


Download IAM policy
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/install/iam_policy.json

Create IAM Policy

aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json

Create IAM Role

eksctl create iamserviceaccount \
  --cluster=my-eks-cluster \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name AmazonEKSLoadBalancerControllerRole \
  --attach-policy-arn=arn:aws:iam::767397700362:policy/AWSLoadBalancerControllerIAMPolicy \
  --approve


Installing eksctl
```
# for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

# (Optional) Verify checksum
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

sudo mv /tmp/eksctl /usr/local/bin
```

![image](https://github.com/user-attachments/assets/e4d201cc-dae4-4b60-9fde-ed051d105eec)


Install helm

```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
helm version

![image](https://github.com/user-attachments/assets/eacabcb4-37e0-48c2-b7dd-7ac798d90014)

Deploy ALB controller

``` helm repo add eks https://aws.github.io/eks-charts ```

``` helm repo update eks```

``` helm install aws-load-balancer-controller eks/aws-load-balancer-controller \            
  -n kube-system \
  --set clusterName=my-eks-cluster \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
  --set region=us-west-2 \
  --set vpcId=vpc-0b1557cc1549be9be
```
