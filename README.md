# kubernates
This repo is to setup kubernates environment on AWS. This contains files generated from other tutorials and few self generated files for educational purpose

# Installation of kubernates on AWS (All the below said activities can be done using the cloud formation)
## Creation of IAM User and assignment of proper roles.
### Creation of IAM User
   1. Services -> IAM -> Users -> Add User
   2. Enter "User Name" and select
     1. Programmatic access
     2. AWS Management Console access
      
   1. Create am IAM account
      1. It is not a good policy to use root account
      2. Create the IAM Account ()
   - Creation of VPC
   - Creation of Subnet
   - Creation of Internet Gateway
   - Creation of Routing Table
   - Association of routing table to all Subnets
   - Creation of security Group