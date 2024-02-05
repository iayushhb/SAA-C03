# Backing up Data with S3 Replication
Replication enables automatic, asynchronous copying of objects across Amazon S3 buckets. Buckets that are configured for object replication can be owned by the same AWS account or by different accounts. You can replicate objects to a single destination bucket or to multiple destination buckets. The destination buckets can be in different AWS Regions or within the same Region as the source bucket.
1. You can replicate objects from one bucket to another,
Versioning must be enabled on both the source and destination buckets.
2. Objects in an existing bucket are not replicated automatically,
Once replication is turned on, all subsequent updated objects will be replicated automatically. *Upload objects after turning on the replication*
3. Delete markers are not replicated by default, 
Deleting individual versions or delete markers will not be replicated.*If you delete an item in the source bucket then the object in the destination bucket will not be deleted*