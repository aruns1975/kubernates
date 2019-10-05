# kubernates
This repo is to setup kubernates environment on AWS. This contains files generated from other tutorials and few self generated files for educational purpose

# Installation of kubernates on AWS (All the below said activities can be done using the cloud formation)
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
### Assignment of policies o the user
   1. Services -> IAM -> Users
   2. Select the user created in "Creation of IAM User".
   3. Click on Add Permission
   4. Click on "Attach existing policies directly"
   5. Select the following policies
       1. AmazonEC2FullAccess
       2. IAMFullAccess
       3. AmazonVPCFullAccess
       4. EKS policy created using "Creation of policy (EKS)" 
       5. EKS policy created using "Creation of policy (Cloud Formation Policy)"
      