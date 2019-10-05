# kubernates
This repo is to setup kubernates environment on AWS. This contains files generated from other tutorials and few self generated files for educational purpose

# Installation of kubernates on AWS
## Creation of IAM User and assignment of proper roles.
### Creation of IAM User
   1. Services -> IAM -> Users -> Add User
   2. Enter "User Name" and select
      1. Programmatic access
      2. AWS Management Console access
   3. Select default values in all subsequent page
### Creation of policy (EKS)
   1. Services -> IAM -> policies -> Create Policy
   2. For the Service select EKS and All EKS Actions
   3. For the Resources select All Resources
   4. Click on Review Policy and create the policy
   5. Sample jSON
```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": "eks:*",
                "Resource": "*"
            }
        ]
    }
```
### Creation of policy (Cloud Formation)
   1. Services -> IAM -> policies -> Create Policy
   2. For the Service select Cloud Formation and All CloudFormation Actions
   3. For the Resources select All Resources
   4. Click on Review Policy and create the policy
   5. Sample jSON
```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": "cloudformation:*",
                "Resource": "*"
            }
        ]
    }
```
### Assignment of policies to the user
   1. Services -> IAM -> Users
   2. Select the user created in "Creation of IAM User" and goto "Permissions" tab.
   3. Click on Add Permission
   4. Click on "Attach existing policies directly"
   5. Select the following policies
       1. AmazonEC2FullAccess
       2. IAMFullAccess
       3. AmazonVPCFullAccess
       4. EKS policy created using "Creation of policy (EKS)" 
       5. EKS policy created using "Creation of policy (Cloud Formation Policy)"
### Creation of EKS Role
    1. Services -> IAM -> Roles
    2. Create Role -> EKS -> Next -> Next -> .... Provide a Name -> Create Role
### Generation of the SSH keys
    1. Services -> E2C -> Key Pairs
    2. Create Key Pair -> Provide a name -> Download the .pem file
    3. the .pem cannot be downloaded again by any manner, thus need to create it again in case if the file is deleted.
### Creation of Access keys
   1. Services -> IAM -> Users
   2. Select the user created in "Creation of IAM User" and goto "Security credentials" tab.
   3. Click on "Create Access key" and "Download .csv" file button.
   4. This downloads the access key which contains the "Access key ID" and "Secret access key"
   5. This file cannot be downloaded again and the "Secret access key" cannot be retreived again by any chance.
## Creation of the VPC, subnets and other networking infrastructure.
### Terminalogies
   1. VPC - Virtual Private Network (Your own private data center with in AWS)
   2. Subnets - For data isolation
   3. Internet Gateway - For accessing the public network from AWS system
   4. Routing Table - To make sure that the subnets are aware of how to connect to internet using the Internet Gateway
   5. Cloud Formation - It is a service which allows to create the infrastucture required using the config file.
### Cloud Formation config file
   1. The cloud formation yml file for the creation of VPC is placed under folder "cloud-formation/EKS-VPC-Cloud-Formation-Template.yml"
### Creation of basic infrastruture using Cloud Formation
   1. Services -> CloudFormation -> Create Stack
   2. Select "Template is ready" and "Upload a template file" -> Choose File and select the file "cloud-formation/EKS-VPC-Cloud-Formation-Template.yml"
   3.  Click next
   4. Provide the Stack Name "My-ekS-vpc-stack"  
   5. Specify the CIDR block for the VPC and the Subnets.
       1. The CIDR block for the subnet should belong to the subset of the VPC
   6. Click Next and click on "Create Stack"
## Creation of Kubernates(EKS) Cluster (Control plane)
   1. Services -> EKS -> Clusters
   2. Create Clusters and enter the following parameters
       1. Cluster Name
       2. Kubrenates version (default should be ok)
       3. Role. Select the role created using "Creation of EKS Role"
       4. VPC. Select the VPC created using the cloud formation
       5. Subnets. Select all the subnets created using the cloud formation
       6. Security Group. Select the Security Group created by cloud formation 
   3. Click on the "Create".
## Installation of client on laptop or desktop
### Required Softwares
   1. Kubectl
       1. This is the client program to manage the kubernates cluster. The user can interact with the kubernated master using the kubectl
       2. Install any terminal emulator like "Mobaxterm' and open the terminal emulator 
       3. curl -k -# -o kubectl.exe https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/windows/amd64/kubectl.exe
       4. chmod +x kubectl.exe
       5. mkdir $HOME/bin
       6. mv kubectl.exe $HOME/bin
       7. echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
       8. source .bashrc
       9. check: ```kubectl.exe version --short --client```
   2. AWS CLI
       1. This program is used to interact with the AWS infrastructure programmatically or using commands
       2.
   3. aws-iam-authenticator
       1. This program is used to perform authenticatin of EKS using the Access Key and Secret Access Key
       2. Install any terminal emulator like "Mobaxterm' and open the terminal emulator 
       3. curl -k -# -o aws-iam-authenticator.exe  https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/windows/amd64/aws-iam-authenticator.exe
       4. chmod +x aws-iam-authenticator.exe
       5. mv aws-iam-authenticator.exe $HOME/bin
       6. Test: ```aws-iam-authenticator.exe help```
   4. Configuring aws-iam-authenticator
       1. Create the folder ".aws" under the user home (C:\users\<username>).
       2. Copy the file "client/credentials" to the folder ".aws"
       3. Edit the file credentials and provide value for the the following properties.(these values are generated and downloaded using the "Creation of Access keys")
           1. aws_access_key_id
           2. aws_secret_access_key 
    5. configuring kubectl
       1. Create the folder ".kube" under the user home.
       2. Copy the file "client/kube-config-eks" to the folder ".kube"
       3. Edit the file "kube-config-eks" and provide value for the following properties. (These values are generate uring the step "Creation of Kubernates(EKS) Cluster (Control plane)")
           1. endpoint-url
           2. base64-encoded-ca-cert
           3. cluster name
       4. Step to test the configuration
          ```kubectl get svc ```
     