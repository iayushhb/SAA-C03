# What is IAM ?
![alt text](/Photos/aws-iam.png)


### IAM allows you to manage users and their level of access to the AWS console.
*IAM offers a centralized hub of control within AWS and integrates with all other AWS Services.*

- Create users and grant permissions to those users.
- Create groups and roles.
- Control access to AWS resources.

## What is root account ? 
The root account is the email address you used to sign up for AWS. The root account has full administrative access to AWS. **For this reason, it is important to secure this account**.

## 4 Steps to Secure Your AWS Root Account.
- Enable multi-factor authentication on the root account.
- Create an admin group for your administrators, and assign the appropriate permissions to this group.
- Create user accounts for your administrators.
- Add your users to the admin group.

## How do we control permissions ?
We assign permissions using policy documents , which are made of JSON(**JavaScript Object Notation**).

The documented rule sets that are applied to grant or limit access. In order for users, groups, or roles to properly set permissions, they use policies. Policies are written in JSON and you can either use custom policies for your specific needs or use the default policies set by AWS.

*Example of a Policy Document:*
![Alt text](/Photos/Json-eg.png)

**`IAM` is Universal*

**User has no permission when first created*

*Access ID and secret keys aren’t the same as username and passwords. And only get to see them once , so save them in a secure location.

*Always set up password rotations & you can create and customize your own rotation policies.


## The Building Blocks of IAM : 
`User` :  any individual end user such as an employee, system architect, CTO, etc.

`Groups` : any collection of similar people with shared permissions such as system administrators, HR employees, finance teams, etc. Each user within their specified group will inherit the permissions set for the group.

`Roles` : any software service that needs to be granted permissions to do its job, e.g- AWS Lambda needing write permissions to S3 or a fleet of EC2 instances needing read permissions from a RDS MySQL database.

> It's best practice for users to *inherit permissions* from groups. And that’s because if you didn’t then it would harder to manage people individually.

![Alt text](/Photos/policy-eg-iam.png)

> Always work on the principle that one user equals one physical person. Never share user accounts across multiple people.

## The principle of least privilege : 
Only assign user the **minimum** amount of privileges they need to do their job.

### Example:
![Alt text](/Photos/iam-eg.png)


### Priority Levels in IAM:
Explicit Deny: Denies access to a particular resource and this ruling cannot be overruled.

Explicit Allow: Allows access to a particular resource so long as there is not an associated Explicit Deny.

Default Deny (or Implicit Deny): IAM identities start off with no resource access. Access instead must be granted.