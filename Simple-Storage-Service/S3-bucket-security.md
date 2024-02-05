# Securing your bucket with S3 block access policies
### Access Control List **VS** Bucket Policy
![Alt text](/Photos/acl-vs-bp.png)

# Creating a S3 bucket - 
Head over to S3 and hit *create bucket*. And you'll get on this page.
![Alt text](/Photos/s3-bucket-create.png)
Now type a globally unique name for the bucket and select the region you want your data to be deployed.
![Alt text](/Photos/s3-list-buckets.png)
### Uploading files to the created S3 bucket : 
Now click on your bucket name and hit upload.
![Alt text](/Photos/s3-file-upload.png)
![Alt text](/Photos/s3-upload-page.png)
Here you can either upload a full folder or a specific file.

After successfully uploading your file to S3 Now click on your object and click on **Object URL**.
![Alt text](/Photos/s3-access-denied.png)
Now you still can't access your uploaded file and that because currently it's denied for public access.

### Now to make your object publicly accessible (on individual object level) :
1. Go to your bucket > permissions then hit edit on Block public access (bucket settings) button then uncheck the Block all public access box and hit save.
2. Now scroll down to Object Ownership, hit edit then check ACLs enabled. Then hit acknowledge button and finally hit save.
3. Now go to objects > Actions > Make public using ACL. Hit make public and done.

> Now you can access your object publicly using object URL.