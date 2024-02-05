# Create and Assume Roles in AWS

> You can either user pre-built policies by aws or you can create a custom policy.

### Now we're gonna restrict access of user1 to every service except S3 bucket:

1. To do that just head to IAM > Policies and hit create policy.
2. Now search S3 and check all S3 actions and check all boxes in resourse section except bucket.
3. To restrict S3 bucket access click on `Add ARN` and paste bucket name. Do this for all buckets you want access to be denied.
   ![Alt text](/Photos/policy-page-iam.png)
4. Now hit next and name the bucket and done.

### Attaching Created Policy to user:

1. Head over to IAM > Policies and select the created policy.
2. Go to `Entitles attached` and hit attach a permission policy button.
   ![Alt text](/Photos/iam-policy-attach.png)
3. Now select user you want this policy attached to and hit attach policy and done.

> Now our user have access to certain S3 bucket and have zero access to other services.