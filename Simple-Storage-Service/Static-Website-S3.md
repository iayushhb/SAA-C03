# Create a Static Website Using Amazon S3

In this Lab we'll create a and configure a simple static website using S3.

We'll also go through configuring that static website with a custom error page and demonstrating a very cost-effective website hosting for sites that consists just HTML, CSS, JavaScript, fonts & images basically static websites.


1. First we're gonna configure an S3 bucket for website hosting.

    **bucket must have public read access enabled.*

2. Uploading the content (download the files from the resource section)
3. Now enable static website hosting by going into the Properties section bottom.
![Alt text](/Photos/static-site-hosting-option.png)
**Now if we scroll back down to static website hosting we'll see a url with our bucket's name.**
![Alt text](/Photos/staic-site-url.png)

Now if try clicking on the url we'll see a 403 Forbidden message which simply means that the site is running but we haven't explicity allowed permission to read the files that are contained in a bucket.

So now , to make our objects publicly accessible we need to add a bucket policy.

4. So now go to the bucket > permissions and edit bucket policy.
5. Now copy bucket ARN.
6. To create our policy we're gonna use the policy generator.
![Alt text](/Photos/s3-policy-generator.png)
7. Select S3 bucket policy for policy type.
8.  - Effect : Allow
    - Principle : *
    - Actions : GetObject
9. Paste ARN with suffix /*
10. Then click add statement 
11. And then click Generate Policy
![Alt text](/Photos/s3-policy-overview.png)
12. Now copy the entire policy and go back to the aws console. And paste the policy.

Now hit save changes and refresh the page and then go the static site url and you'll see the website working.
![Alt text](/Photos/final-static-site.png)