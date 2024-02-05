# AWS Command Line
You can also interact with AWS using the Command Line.

*Objective :*
- Launch an EC2 instance to use the aws cli
- Create an IAM User and give the user permission to access and create S3 resources
- Configure the cli using the IAM user's credentials. Then use the cli to create an S3 bucket and upload a file.

## Launching an EC2 instance - 
1. Head to EC2 and hit launch instance.
2. Now select your created instance and hit "ACTIONS" and select connect. 

![Alt text](/Photos/ec2-connect.png)
Then click connect to access the aws cli.

![Alt text](/Photos/instance-connect.png)

![Alt text](/Photos/aws-cli.png)

**Now to gain root access type :**
```
sudo su
```
**To update the system :**
```
dnf update -y
```
**Now before accessing aws resources you have to configure the system :**
```
aws configure
```
but you'll need access keys to configure so let's create a user who have s3 accessibility

- First create a user group and attach `AmazonS3FullAccess` policy
- Now let's create a user and add it to the created user group
- Now to get the access keys of that user go to the user's Secutiy Credential section and hit create access keys, select use case 'cli'. then save those credentials safely.

Now use those creadentials to configure aws cli.

3. Now to list out your s3 bucket using cli type : 
```
aws s3 ls
```
4. To make bucket type : 
```
aws s3 mb s3://mynewbucket2003ash
```