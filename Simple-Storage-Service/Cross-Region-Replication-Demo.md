# Set Up Cross-Region S3 Bucket Replication

### You can use S3 cross region replication to copy data from one region bucket to another bucket.

[YT video for reference](https://www.youtube.com/watch?v=_6admeBN-lI&ab_channel=AmazonWebServices)

1. Create a source bucket and then create a destination bucket and select another region.
2. Now turn on versioning for both of them.
   ![Alt text](/Photos/replication-bucket.png)
3. Now in the source bucket go to the Management tab and create replication rules.
4. Enter rule name, let's say "rule4s3".
5. Now select Apply to all objects in source bucket section.
   ![Alt text](/Photos/replication-rules.png)
6. Then select your destination bucket in destinaion section.
7. Then select Create new role in IAM role secion.
   ![Alt text](/Photos/replication-destination.png)
8. Now after you can change any other setting you wanna change I'm just gonna leave it as default.
9. Now hit save and you'll get this message since we have no existing objects in our bucket we'll just go ahead say "no" for now.
   ![Alt text](/Photos/replication-rule-alert.png)
   Now hit submit and done.
