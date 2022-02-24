## Infrastructure

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
* `aws cloudformation deploy --profile dev --stack-name test1 --region us-east-2 --template-file ./csye6225-infra.yml ` to create stack
* change `profile` and `region` parameters in the above command as per the use