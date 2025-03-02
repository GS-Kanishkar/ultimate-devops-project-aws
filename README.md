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





