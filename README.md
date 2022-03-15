## Infrastructure

## Assignment - 03
## Steps to create Dev and Demo profiles for resource creation using AWS Cloud Formation

1. Sign-in to AWS (Dev Account) console
2. Create a user with administrative privileges in IAM
3. Go to the Security credentials of the user created, and save the Access key Id and Secret Id
4. Repeat step 2 and 3 by signing in to AWS(Demo Account) as well
5. Install CLI from https://docs.aws.amazon.com/cli/latest/userguide/awscli-install-linux.html and run aws --version to check if the installation is done right.
6. In the terminal run, `cd ~` and `cd .aws` commands
7. Now run `aws configure`
8. Enter the `Access key ID` , `Secret Access Key` from Dev account user credentials (From step 2 and 3)
9. Enter the `Default region name` (Mostly us-east-1) and `Output Format` ( `json` or `yml` ) fields
10. `aws configure --profile=dev` will create a dev profile, and repeat the step number 8.
11. `aws configure --profile=demo` will create a demo profile, and repeat the step number 8 with demo account credentials.
12. `vi config` or `vi credentials`


## Describe VPCs
* `aws --profile=dev ec2 describe-vpcs`
* Also, we can use `export AWS_PROFILE=dev` or `export AWS_REGION=us-east-1` and then run `aws ec2 describe-vpcs`
* Use `env` to verify the profile and other detail


## AWS Networking Commands
* To create a stack : `aws cloudformation deploy --profile dev --stack-name test1 --region us-east-2 --template-file ./csye6225-infra.yml ` 
* change `profile` and `region` parameters in the above command as per the use
* To delete the stack, use the command :  `aws cloudformation delete-stack --profile dev --stack-name test1 --region us-east-2 ` 
  
## Assignment - 05
* The goal of this assignment is to: create an EC2 instance, attach the RDS instance profile to it and use the MYSQL available in the AWS.
* The flow is : 
    - Create3 private subnets in the existing VPC
    - Created a private route table and necessary route table association for private subnets
    - Created a DB subnet group referencing all 3 private subnets
    - Created a EC2 security group(For RDS),which has the reference to `application security group` created in Assignment-03. It has a inbound 
    - Create a RDS instance and attach the parameter group , subnet group and EC2 security group(For RDS) to it
    - Create a policy to create, get and delete the objects and create an IAM role; Attach the policy to the newly created IAM role.
    - Create  a Instance profile for S3 bucket which has the reference to the S3 bucket and attach the IAM role to this profile
    - Now Add the RDS Instance and S3 bucket profile to the EC2 Instance

## Commands to create stack
- Create a stack `aws cloudformation deploy --profile dev --stack-name assignment5 --region us-west-2 --template-file ./csye6225-infra.yml --capabilities CAPABILITY_NAMED_IAM `
- Delete a stack `aws cloudformation delete-stack --profile dev --stack-name test1 --region us-east-2`
- Delete S3 Bucket `aws s3 rm s3://soumyanayar3-dev.soumyanayar.me --recursive`
- `aws cloudformation validate-template --template-body file://Templates/csye6225-infra.yml --region us-west-2 ` To validate the template