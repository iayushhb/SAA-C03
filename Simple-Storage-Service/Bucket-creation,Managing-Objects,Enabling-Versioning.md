# Creating Amazon S3 Buckets, Managing Objects, and Enabling Versioning


## Creating buckets
1. Create a new public bucket with ACL enabled and public read access enabled.
2. Create a new private bucket i.e. block all public access.
3. Now upload single picture of cat in both of these buckets(get pics from resource section).
4. So for private bucket if you tried to access the content by going into object and clicking the oject url you'll get an error.(cuz the bucket is not publically accessible)
![Alt text](/Photos/s3-access-denied.png)
But for public bucket go to object then hit object actions and hit enable using ACL then you'll see your uploaded content.
![Alt text](/Photos/object-overview.png)
![Alt text](/Photos/cat-image.png)

## Creating versions for that same file
Now to enable versioning head to bucket > properties and enable versioning.
1. Now upload the file with the same name to the bucket.
2. Now to see versions of your file hit the show versions button.
![Alt text](/Photos/versions-ui.png)