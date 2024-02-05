# Roles in AWS
An IAM role is an IAM identity that you can create in your account that has specific permissions. An IAM role is similar to an IAM user, in that it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it. Also, a role does not have standard long-term credentials such as a password or access keys associated with it. Instead, when you assume a role, it provides you with temporary security credentials for your role session.

## Creating an IAM role 

To create an IAM role head over to IAM > Role and hit create role
![Alt text](/Photos/roles-iam.png)
and now select aws service and for usecase let's just go with ec2 

Now select permissions you want to give : here I am giving S3 full access.
![Alt text](/Photos/roles-permissions.png)

Now name review and create - 
![Alt text](/Photos/role-final.png)

### Using the created role

To use your role that your created head over to ec2 and create an instance then select your created ec2 instance and hit actions > security > Modify IAM role and select the role that  
![Alt text](/Photos/modify-iam-role.png)

Now let's connect with the ec2 instance using ec2 instance connect

![Alt text](/Photos/role.png)

as you can see when the role is attached you don't have to give your credentials.